# OpenSSL upgrade process
OpenSSL is a cryptographic library used for secure communication over networks.
[Reference](https://linuxhint.com/update-open-ssl-raspberry-pi/)
* Check OpenSSL version
  ```BASH
  openssl version
  ```
  The latest version of OpenSSL at the time of writing this file is “3.1.0”
* Install dependencies
  ```BASH
  sudo apt install build-essential zlib1g-dev checkinstall -y
  ```
* Change the location
  ```BASH
  cd /usr/local/src/
  ```
* Download OpenSSL Latest Version Source File.  
  Go to the [website](https://www.openssl.org/source/) to download OpenSSL latest version source file.
  ```BASH
  wget https://www.openssl.org/source/openssl-3.1.0.tar.gz
  ```
* Extract Content of OpenSSL Source File
  ```BASH
  sudo tar -xf openssl-3.0.7.tar.gz
  ```
* Navigate to OpenSSL Directory
  ```BASH
  cd openssl-3.0.7
  ```
* Configure OpenSSL
  ```BASH
  sudo ./config --prefix=/usr/local/ssl --openssldir=/usr/local/ssl shared zlib
  ```
  The above command sets up the path for OpenSSL, creates a shared library and enables compression using the zlib library.
* Navigate to OpenSSL Directory
  ```BASH
  cd openssl-3.0.7
  ```
* Compile the OpenSSL Files
  ```BASH
  sudo make
  ```
* **Install OpenSSL**
  ```BASH
  sudo make install
  ```
* Configure Shared Libraries for OpenSSL  
  OpenSSL loads the binary files from the location “/usr/local/ssl/lib” and you have to configure this path. First, navigate to the following directory:
  ```BASH
  cd /etc/ld.so.conf.d/
  ```
  Create a configuration file through the nano editor using the following command:
  ```BASH
  sudo nano openssl-3.0.7.conf
  ```
  Append the following location inside the file.
  ```BASH
  /usr/local/ssl/lib
  ```
  Save this file using `CTRL+X`.  
  Reload the changes through the following command:
  ```BASH
  sudo ldconfig -v
  ```
* Replace the Default OpenSSL Libraries  
  You must replace the previous default OpenSSL libraries with the new ones, but before that, you must create the files backup by running the following commands one by one.
  ```BASH
  sudo mv /usr/bin/openssl /usr/bin/openssl.BEKUP
  sudo mv /usr/bin/c_rehash /usr/bin/c_rehash.BEKUP
  ```
  Afterward, you have to edit the `/etc/environment` file:
  ```BASH
  sudo nano /etc/environment
  ```
  Inside the file, paste the following text:
  ```BASH
  PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/local/ssl/bin"
  ```
  Save the file and then load the changes using the following command:
  ```BASH
  source /etc/environment
  ```
  Test the path through the following command:
  ```BASH
  echo $PATH
  ```
* Ensure that OpenSSL is successfully updated
  ```BASH
  openssl version
  ```



