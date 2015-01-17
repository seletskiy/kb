### Setting up vim autocompletion via eclipse (usually for Java)

* Install eclim package (with eclipse):  
  https://aur.archlinux.org/packages/eclim
* Add following line to `.vimrc`:
  ```viml
  let g:EclimCompletionMethod = 'omnifunc'
  ```
* Either start `eclimd` manually or via user systemd service:
  `$ /usr/share/eclipse/eclimd`
* Create `.project` inside your project dir with following contents:
  ```xml
  <projectDescription>
      <name>PROJECTNAME</name>
  </projectDescription>
    ```
* Open vim, cd to project directory and run:
  `:ProjectCreate . -n java`

* *(Android development)* Add line like that (with needed API version) to
  `.classpath` at the project dir:
  ```xml
  <classpathentry kind="lib" path="/opt/android-sdk/platforms/android-19/android.jar"/>
  ```
