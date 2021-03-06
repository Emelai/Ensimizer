# Ensimizer
## Introduction
Ensimizer allows you to creat a mock sbt directory structure for an Ammonite script project directory. This allows you to edit the scripts as Scala code in text editors that work with [Ensime](http://ensime.org/) or the new sbt support for VS Code's Language Server Protocol.For ensime, it uses [Ensime's sbt plugin](http://ensime.org/build_tools/sbt/). The only editor this has been tested on is Visual Studio Code, but there is no reason it shouldn't work in other editors. **NB:** keep in mind that because Ammonite is not pure Scala, the  code highighting won't work as well as it does for regular Scala files.
## How It Works
Essentially the script creates an sbt project structure, and then creates links to the Ammonite scripts in the `src/main/scala` directory. These links have a `.scala` extension so when you open those files in your Ensime supporting text editor or VS Code with either Ensime or SBT LSP plug-in, they are recognized as Scala files.

In order for this to work with Ensime, you need to first add the Ensime sbt plugin to the appropriate sbt file  as per the instructions [here](http://ensime.org/build_tools/sbt/#install). If you use the "ensime" target (see below), the last line of the script runs `sbt ensimeConfig` so you don't have to.

To run the script you go into the project directory where your Ammonite scripts are found and issue this command in your shell:

`amm /directory/which/has/script/Ensimizer.sc ensimize "<target>"`

where target is either "ensime" or "sbt"

If you wish to cleanup all the added files run this command in your shell:

`amm /directory/which/has/script/Ensimizer.sc unEnsimize`

If you wish to ensimize a new script in your directory run this command in your shell:

`amm ~/Scripts/Ammonite/Ensimizer.sc scalaIt "<filename>.sc"`

The Ensimizer Ammonite script uses Ammonite Ops so your `predefScript.sc` file must include the following line:
`import ammonite.ops._, ImplicitWd._`

## Current Caveats
In this version of the script, there are several things you need to do manually. In future versions the script will provide ways to do this for you.
1. If you want to check in your scripts into github without all the added scaffolding, copy the `.gitignore` file from the cloned project into your project directory. The ensimizer project was used on itself and as you can see only the script is in the project.
2. The version of Scala and SBT are hard-coded & need to be manually updated if Ensime/SBT changes support for specific versions.

 

