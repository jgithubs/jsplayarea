Doxygen needs to be install before creating documentation.

1. Download and unzip. Suggest using the zip file because it does not require administration privilages.

2. Rename the binary directory to 'Doxygen'. In this case, the direction is at the C drive level.

3. Add directory to the PATH environment.

4. Open a new dos shell and type 'PATH'. The last entry in the path should be the added path.

5. Test the doxygen executable by typing 'doxygen --version'

6. Go to the directory where the 'doxyConfig' file exists.

7. Create the documentation with 'doxygen doxyConfig'

8. Open up ./Doxyoutput/html/index.html with a browser.

9. The documentation for the project is now accessable.