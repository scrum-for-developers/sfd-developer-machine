# sfd-developer-machine
Vagrant/Ansible Project to set up a developer machine containing IDEA and Eclipse for the "Scrum for developers" training hold by [codecentric AG](https://www.codecentric.de).

## Setup
Assuming you have [Vagrant](https://www.vagrantup.com/) already installed on your machine just checkout the repository, enter the checked out directory and run

```vagrant up```

### Things installed by Vagrant/Ansible
  * Ansible itself
  * git
  * zsh
  * curl
  * openjdk-8-jdk
  * maven
  * vim
  * mysql-server
  * python-mysqldb (for database creation via Ansible)

### Other stuff that happens
  * Ansible downloads IntelliJ Community Edition and Spring Tool Suite from Centerdevice (because URLs don't change there).
  * It unzips it to
    * ```/opt/IntelliJ```
    * ```/opt/Eclipse```
  * Global Path to Java8 gets set
  * Desktop links and necessary folders get created
  * The worblehat database get's created with
    * user: worblehat
    * password worblehat

### Things you still need to to by hand
These steps are recommended if you want to provide a ready-to-go VM to training participants. Execute them inside the VM.
  * Open a terminal and checkout the [worblehat application](https://github.com/scrum-for-developers/worblehat).
  * Do a ```mvn clean install``` inside the application path to download all necessary dependencies, so that the participants don't need to anymore, which speeds up the training.
  * Remove the checked out project afterwards (The training participants get their own copies of the repository).
  * Optional (**Attention:** You shouldn't use the installed IDEAs for the optional tasks. Otherwise you'd create personalized settings which shall be left for the training participants.)
    * Enter ```worblehat-web``` and run ```mvn spring-boot:run``` and check ```localhost:8080/worblehat``` to see if the application works. The application will run against an in-memory database.
    * Modify ```worblehat-web/src/main/resources/application.properties```.
    Remove the hashtags before the database configuration to test if the local database is working. Restart the application and check  ```localhost:8080/worblehat``` again. The application should now run against the installed mysql database.
