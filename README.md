# CS239_tool_presentation

## Tutorial on using GENPROG to fix a simple program
Becuse of the setup cost for configuring a working environmet for GENPROG we suggest using a virtual machine provided by the creators of the tool.

GENPORG documentation page can be found [here](http://dijkstra.cs.virginia.edu/genprog/).
The vitrual machine we will use in this tutorial can be found [here](http://dijkstra.cs.virginia.edu/genprog/resources/autorepairbenchmarks/VirtualMachines/).
Download the contents of 'genprog_icse2012_virtualbox/' and repackage them in a single folder.
If you are using [VirtualBox](http://www.virtualbox.org/) you can mount the image as is.
In case you are using another virtualization software you will need to convert the image.

### Coverting the .vmdk image
Using a tool calld ovf tool, we can convert a .vmdk image to a .vmx image using the following steps:
* download the tool [here](https://www.vmware.com/support/developer/ovf/) from the VMware website. 
* use the tool to convert your image into the desired extension \<path to tool>/ovftool --lax \<folder that contains the image files> \<result>.vmx
