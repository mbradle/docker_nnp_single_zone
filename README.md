# docker_single_zone
This is the Webnucleo single-zone reaction network docker image repository.

# Steps to build and run the default docker image.

First clone the repository.  Type:

**git clone http://github.com/mbradle/docker_single_zone**

Now build the image.  Type:

**cd docker_single_zone**

**docker build -t single_zone .**

Now create a directory for the input and output.  Type:

**mkdir work**

**mkdir work/input**

**mkdir work/output**

**cp input/run.rsp work/input/**

Now download the necessary data.  First, record the current location.  Type

**pwd**

Replace PWD in the instructions below with the string that is returned by
this command.  Now download the data.  Type:

**docker run -it -v PWD/work/input/data_pub:/data_directory -e VAR=data webnucleo/data_download**

Now edit work/input/run.rsp.  Run the calculation.  For example, type:

**docker run -it -v PWD/work/input:/input_directory -v PWD/work/output:/output_directory -e VAR=@/input_directory/run.rsp single_zone**

The output will be in the directory work/output.  One can add options into the response file run.rsp or directly into the command line.  For example, type:

**docker run -it -v PWD/work/input:/input_directory -v PWD/work/output:/output_directory -e VAR="@/input_directory/run.rsp --tend 1." single_zone**

This calculation cuts off the expansion after 1 second instead of the default 1.e6 seconds.

# Steps to build with a different master.h file.

First, download the default master.h to the output directory.  Type:

**docker run -it -v PWD:/header_directory -e HEADER_COPY_DIRECTORY=/header_directory single_zone**

Edit master.h.  Now rebuild, but set the WN_USER flag:

**docker build -t single_zone --build-arg WN_USER=1 .**

Edit work/input/run.rsp appropriately.  Then run as before.
