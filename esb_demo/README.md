## Introduction
This project involves developing an Enterprise Service Bus (ESB) in C. 

### Setting up the development environment
Following instructions assume that you are working on an Ubuntu machine, and are in the sudoers group (or have root access).

### Installing essential libraries that you will need
1, Open a shell and run  `sudo apt update`

2, Ensure that you have installed the essential headers and libraries: `sudo apt install build-essential`

3, You will be writing unit tests for all your C code using [munit](https://nemequ.github.io/munit/).

4, Install Kore Web framework as [described here](https://docs.kore.io/3.3.1/install.html). You will use it to write an HTTP endpoint for receiving the requests for the ESB. NOTE: A skeleton is provided to get you started. However, you are strongly encouraged to go through the [Kore's simple guide](https://docs.kore.io/3.3.1/).


5, Install [curl](https://www.cyberciti.biz/faq/how-to-install-curl-command-on-a-ubuntu-linux/) inorder to send data using various protocols. (SMTP,HTTP used in this project).

6,Install [libxml2](https://askubuntu.com/questions/733169/how-to-install-libxml2-in-ubuntu-15-10), XML library for parsing xml document.

7,Install [Mysql server](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-18-04) inorder to store the records.

### Creating a workspace with the sample code
You can execute the following steps on a shell (on Ubuntu):


#### Install required libraries
sudo apt update

sudo apt install build-essential

sudo apt install libssl-dev

sudo apt install wget

sudo apt install curl

#### Download the kodev sources
wget https://kore.io/releases/kore-3.2.0.tar.gz

tar -xf kore-3.2.0.tar.gz

cd kore-3.2.0/

#### Build and install kodev
make

sudo make install

#### Change directories into a working folder
cd /path/to/where/you/want/to/work

#### Name 'esb_endpoint' is important, because we will be copying the files from this repo
kodev create esb_endpoint

#### Fetch the code from this repositiry
git clone https://github.com/nho2020/esb_proj.git

#### Copy only the relevant files from cloned repo into your kodev created one
cp -r esb_proj/esb_app/src/* esb_endpoint/src/

cp -r esb_proj/esb_app/conf/* esb_endpoint/conf/

#### Build and run the kodev application
1,cd esb_endpoint/

2,kodev build

3,kodev run

4,Open another shell window and run: curl --insecure -F "bmd_file=@/some/file/path/dummy_data.txt" https://localhost:8888/bmd

Check the logs in first shell; it should show that the file was successfully received.
If there is an empty reply (curl(52)),retry with the same command.If such problems still persist,then run kodev once again.

5,For email service ,enter the file name exactly with extension that you want to send (for eg:here it is data-Payload.json)

 SMTP: We are implementing it using curl.Transport key is smtp and transport value is the mail id to whom we are sending the payload after transformation.

6,You also need to allow less secure apps for sending email.Refer [this](https://devanswers.co/allow-less-secure-apps-access-gmail-account/)
