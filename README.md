# CS239_tool_presentation

## Tutorial on using GENPROG to fix a simple program
Becuse of the setup cost for configuring a working environmet for GENPROG we suggest using a virtual machine provided by the creators of the tool.

GENPORG documentation page can be found [here](http://dijkstra.cs.virginia.edu/genprog/).

The vitrual machine we will use in this tutorial can be found [here](http://dijkstra.cs.virginia.edu/genprog/resources/autorepairbenchmarks/VirtualMachines/).


Download the contents of 'genprog_icse2012_virtualbox/' and repackage them in a single folder.

If you are using [VirtualBox](http://www.virtualbox.org/) you can mount the image as is.

In case you are using another virtualization software you will need to convert the image.

### Converting the .vmdk image
Using a tool calld ovf tool, we can convert a .vmdk image to a .vmx image using the following steps:
* download the tool [here](https://www.vmware.com/support/developer/ovf/) from the VMware website. 
* use the tool to convert your image into the desired extension \<path to tool>/ovftool --lax \<folder that contains the image files> \<result>.vmx
* Mount the .vmx file on your favorite virtual machine

### Downloading and moving to virtual machine
You can download [GENPROG source v1](http://dijkstra.cs.virginia.edu/genprog/resources/genprog-source-v1.tar.gz).

In order to copy the .tar file onto your newly mounted machine, you will need to find it's ip address.

We can do that using the 'ifconfig' command on the virtual machine and look in the 'inet addr' field.

In case your network card is not showing you can use the 'ifconfig eth1 up' command to enable your networking device.

Once you have your IP address, use the following command to copy your .tar file onto your virtual machine:

scp \<path to .tar file>/genprog-source-v1.tar root@\<your IP address>:~/

## Using GENPROG to fix a buggy program
The virtaul machine provides us with a buggy implementation of the greatest common denominator along with passing and failing test cases.

The rest of this tutorial will provide the commands you can run to successfully patch this program using GENPROG.

### Compiling the program
from /~:

~~~~
tar -xvf genprog-source-v1.tar
cd genprog-source-v1
make
~~~~

The command we will run to patch a program is "modify".

To view it's paramaters you can run:

~~~~
modify --help
~~~~

### Verifying program performance 

~~~~
cd quad
gcc gcd.c -o run
./run 10 15
~~~~
We expect this to output 5

~~~~
./run 0 55
~~~~
We expect this to output 55 then loop forever, thus exhibiting buggy performance.

### Patching a program

~~~~
../modify --max 15 --good_path_factor 0.01 --seed 0 -- mut 0.6 gcd.c
cd minimize/
gcc best.c -o run
./run 0 55
~~~~
best.c contains the minimized patched program returned by GENPROG.

Running it with the previously failing testcase should now pass.

~~~~
./run 10 15
~~~~
Running with the previously passing testcase should still pass.


### Voila! 
GENPROG has patched our program!


