## Setting up bioinformatics data analysis server on AWS

1. Create Amazon Webservices Account on aws.amazon.com
2. Selected Basic Support level account.
3. Go to AWS management console and sign in as a root user.
4. Select launch virtual machine with EC2.
5. Launched Ubuntu Server 20.04 LTS (HVM), SSD Volume Type 64-bit(x86)
6. Selected instance type t3a.2xlarge with 8 cores and 32G of memory.
7. Keep the settings in [Configure instance] tab at default.
8. Increased storage under [Storage] tab to 16 Gb.
9. Under [Configure Secutiry Group] keep it as SSH, which is a default setting.
10. Review and Launch, in the pop up window select 'create new key pair'. Name and download a key pair. By default a key pair is downloaded as a .pem file. We will need to convert it to .ppk file for use with Putty.
11. The initial request to valudate may take some time to be validated by Amazon.
12. It is useful to create a billing altert to be notified about the charges by email. 

## Connecting to out AWS instance.
1. Convert private key file in .pem format downloaded from Amazon to 
.ppk format usin *PuttyGen* https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html. Make sure not to change the key-pair name, for example if the key-pair file downloaded was *biocomp1.pem* than it should be converted to *biocomp1.ppk* with *PuttyGen*.
2. Get the IP address from AWS panel and use to login into the AWS server with Putty. You'll need to point Putty to key-pair file on .pkk format in [SSG -> Auth] tab.
3. The username to login into Ubuntu server is "ubuntu". If the username does not work, try "root". 

## Configuring the server for bionformatics work.
1. Update and upgrade Ubuntu
```
sudo apt-get update

```
```
sudo apt-get upgrade
```
Install necessary dependencies
```
sudo apt-get -y install make gcc zlib1g-dev libncurses5-dev libncursesw5-dev git cmake build-essential unzip python3-numpy python3-dev python3-pip python-is-python3 gfortran libreadline-dev default-jdk libx11-dev libxt-dev xorg-dev libxml2-dev libcurl4-openssl-dev apache2 csh ruby-full gnuplot cpanminus libssl-dev gcc g++ gsl-bin libgsl-dev apt-transport-https software-properties-common meson libvcflib-dev libjsoncpp-dev libtabixpp-dev
```

## Install bioinfromatics software with Conda

1. Install Miniconda for Linux
Download the installer
```
 wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
 bash Miniconda3-latest-Linux-x86_64.s
```
Run the installer and follow the prompts.
Restart the session for the changes to take effect.
Create new conda environment names 'varcall'.

```
conda create -n varcall
```
Activate the newly created environment.

```
conda activate varcall
```
2. Install SRA toolkit
```
 conda install -c bioconda sra-tools
```

3. Install FastQC.
```
conda install -c bioconda fastqc
```
4. Install QualiMap
```
conda install -c bioconda qualimap
```

5. Install TrimGalore!
```
conda install -c bioconda trim-galore```

```
6. Install BWA (aligner).
```
conda install -c bioconda bwa
```
7. Install the variant caller (GATK).
```
conda install -c bioconda gatk
```
