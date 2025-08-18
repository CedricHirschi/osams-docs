XSCHEM currently does not work for cosimulation out of the box. Ngspice (vvp specifically) is not able to find certain library files.

There are two ways to fix this. One easy way if you have sudo rights, one more complex if you dont.

## Easy Fix (with sudo rights)

If you have sudo rights, you simply copy the library files to the place ngspice expects them to be. The commands for that are:
```bash
sudo mkdir -p /usr/local/lib/ngspice
sudo cp /foss/tools/ngspice/lib/ngspice/ivlng.vpi /usr/local/lib/ngspice
sudo cp /foss/tools/iverilog/lib/libvvp.so /foss/tools/ngspice/lib/ngspice
```

## Complex Fix (without sudo rights)

If you don't have sudo rights, we use `proot` to emulate the necessary environment. For this, we create a script to set up this environment:
```bash title="proot.sh"
# one-time prep
echo "Copying ngspice files..."
mkdir -p "$HOME/.local/lib/ngspice"
cp --update=older /foss/tools/ngspice/lib/ngspice/ivlng.vpi "$HOME/.local/lib/ngspice/"
ln -sf ivlng.vpi "$HOME/.local/lib/ngspice/ivlng"   # optional

if ! command -v proot >/dev/null 2>&1 && [ ! -f "$HOME/bin/proot" ]; then
    echo "Installing proot..."
    mkdir -p "$HOME/bin"
    curl -L -o "$HOME/bin/proot" https://proot.gitlab.io/proot/bin/proot
    chmod +x "$HOME/bin/proot"
else
    echo "proot already available, skipping installation."
fi

# wrapper
echo "Creating xschem-proot wrapper..."
mkdir -p "$HOME/bin"
cat > "$HOME/bin/xschem-proot" <<'SH'
#!/usr/bin/env bash
LIB="$HOME/.local/lib/ngspice"
# let vvp find its loader too (usually already OK)
export LD_LIBRARY_PATH="/foss/tools/iverilog/lib:${LD_LIBRARY_PATH}"
exec "$HOME/bin/proot" \
  -b "$LIB:/usr/local/lib/ngspice" \
  xschem "$@"
SH
chmod +x "$HOME/bin/xschem-proot"
export PATH="$HOME/bin:$PATH"

echo "Done!
Use the new \`xschem-proot\` wrapper to run xschem with cosimulation support."
```

Then, source this script:
```bash
source ./proot.sh
```
And every time you want to run xschem with cosimulation support, use the `xschem-proot` wrapper instead of the regular `xschem` command.