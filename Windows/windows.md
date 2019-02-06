# Windows

### Windows Incompatible Files

Certain file names that work on Mac are not compatible with Windows. This is an issue if you create such a file on Mac, commit to GitHub, and then try to clone that repository to Windows. If you have an issue, the first thing to check is file compatibility. On Mac/Linux, run the following command to identify any problematic files:

`find . -name '*[<>:"/\\|?*]*'`

Rename these files to a Windows compatible format and re-commit.
