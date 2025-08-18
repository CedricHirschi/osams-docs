If you have an ETH internal account and have access to the `oseda` tool, you can use it directly. This is basically a wrapper for a _IIC-OSIC-TOOLS_ container.

There are some considerations to be made: `oseda` does not automatically set up some stuff that _IIC-OSIC-TOOLS_ normally does. This includes:
- The `PDK_ROOT` environment variable: Specifies where the PDKs are located
- The `PDK` environment variable: Specifies which PDK we are using
- The `~/.xschem/xschemrc` file: There, we have a command for setting up SG13G2 PDK specific stuff for XSCHEM

To set the environment variables, I suggest setting up a `ethz.env` file with the following content:
```bash
#!/bin/sh

export PDK_ROOT="/foss/pdks"
export PDK="ihp-sg13g2"
```

To fix your `~/.xschem/xschemrc`, add the following line to the end of it (WITHOUT changing the other content):
```tcl
source $::env(PDK_ROOT)/$::env(PDK)/libs.tech/xschem/xschemrc
```


To use the tools you either prefix all commands you enter
```bash
oseda bash
```
to enter a shell where everything is set up. Then, you first source the `ethz.env` file via
```bash
source ethz.env
```
Now, you should be able to use all tools.