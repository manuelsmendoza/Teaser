To try out the Teaser web application, please head to [http://teaser.cibiv.univie.ac.at](http://teaser.cibiv.univie.ac.at).

# Teaser
Welcome to the official Github page of Teaser, an analytical framework for benchmarking NGS read mappers. Teaser allows researchers to identify the optimal mapper, parameter set and mapping quality thresholds for data sets that mimic their real data. Teaser is easy-to-use, flexible and fast thanks to its genome subsampling process, allowing users to test a variety of scenarios within minutes. Teaser is available as [web application](http://teaser.cibiv.univie.ac.at), a [virtual machine image](https://github.com/Cibiv/Teaser#advanced-users-virtual-machine-image) and as [installable version](https://github.com/Cibiv/Teaser#advanced-users-installation).

###Citation
If you use Teaser to optimize read mapping in your study, please consider citing: Smolka M, Rescheneder P, Schatz MC, von Haeseler A and Sedlazeck FJ. Teaser: Individualized benchmarking and optimization of read mapping results for NGS data. Genome Biology 2015, 16:235 (22 October 2015). DOI: 10.1186/s13059-015-0803-1

# Quickstart
Getting started with Teaser takes just a few minutes. The following sections contain possible next steps for beginners and advanced users.

## Example Report
For every benchmark Teaser generates an interactive HTML report summarizing the accuracy and performance of each mapper. A good way to get an overview of some of the features of Teaser could be to browse such a report. For an example, here Teaser was used to test five mappers on a [D. melanogaster Ion Torrent resequencing](http://teaser.cibiv.univie.ac.at/static/dataset_gallery/D3_n.html).

## Web Application
To quickly get started with testing mappers for a personalized data set, Teaser is available as a public [web application](http://teaser.cibiv.univie.ac.at) that requires no registration.

## Learning more
For topics such as adding support for new mappers or creating customized parameter sets or even test procedures, please see our [Github Wiki](https://github.com/Cibiv/Teaser/wiki) for detailed information regarding the usage and extension of Teaser.

## Advanced Users: Virtual Machine Image
Using a local version of Teaser enables features such as adding new reference genomes, parameter sets, mappers and importing custom read data. We provide a ready-to-go installation as a virtual machine image in Open Virtualization Format (OVA).

The Teaser virtual machine image is available for [download](http://www.cibiv.at/software/teaser/Teaser_current.ova) (2.4GB) from the CIBIV servers. The image is tested for compatibility with [VirtualBox](https://www.virtualbox.org/).

Please note that the memory limit of the machine may have to be adapted, especially when mapping reads to large reference genomes.

The image contains a pre-installed default version of Teaser. Please consult the documentation in the [Github Wiki](https://github.com/Cibiv/Teaser/wiki) for details on the usage and extension.

## Advanced Users: Installation
For advanced users we recommend installing Teaser directly on your computer. Using the virtual machine / installed version of Teaser enables features such as adding new reference genomes, parameter sets and mappers. Teaser is bundled with an installation script that will download and install a predefined set of read mappers and read simulators.

Requirements:
* UNIX-like Operating System
* Python 2.x

Packages that may need to be installed before downloading and installing Teaser:
* python-pip
* python-dev

Packages that may be needed for the automatic building of mapper binaries:
* build-essentials (gcc,g++,etc.)
* cmake
* zlib

Installation:
```
git clone https://github.com/Cibiv/Teaser.git
cd Teaser
./install.py
```

##Adapting Teaser: Adding new References, Parameter Sets and Mappers
A main reason for using a local version (virtual machine image or installation) is the ability to further customize Teaser.

###Adding a reference sequence
To add your desired reference sequence to Teaser, simply copy the FASTA file into the `Teaser/references` directory. Afterwards, you will be able to select the newly added reference on the web interface data set creation page.

When mapping reads to a reference sequence for the first time, mappers may require a significant amount of time for building the reference index. To reduce this, we provide the complete set of index files bundled with the original refrence for selected organisms at http://www.cibiv.at/software/teaser/references. After downloading the package for your desired reference genome, simply extract the archive and place all the files in the `Teaser/references` directory. 

###Adding new parameter sets and mappers
For adding community parameter sets or mapper definitions, copy the downloaded YAML files in the `Teaser/setups` directory. Teaser will automatically load them after which they will be available for selection in the web interface.

The respective Wiki pages explain how to [create new parameter sets](https://github.com/Cibiv/Teaser/wiki/Mapper-Parameters) and add [support for new mappers](https://github.com/Cibiv/Teaser/wiki/Mappers) from scratch.

###Importing Data Sets
To import custom or real read data sets, place the data files in the `Teaser/import` directory. You will then be able to select the files to import in the web interface.

##Starting a Local Web Interface
The web interface can be started locally and is sufficient for most tasks, including benchmarking newly added reference genomes, mappers and parameter sets.

To start the web interface, execute the following command in the main Teaser directory:
```
./server.py
```

In order to access the web interface, open the following URL in a web browser of your choice: `http://localhost:8888`. In case the web interface was started on another machine, replace `localhost` with the hostname of that machine.

##Command-Line Usage
The virtual machine and installed versions of Teaser can be used from the command-line. The command-line version of Teaser is controlled using configuration files in YAML format. The [Command Line](https://github.com/Cibiv/Teaser/wiki/Command-Line) Wiki page includes examples on how configuration files can be used to define data sets and control benchmarks.

Example usage: Running the built-in E. coli example benchmark:
```
./teaser.py example_ecoli.yaml
```

Example usage: Running the built-in E. coli example benchmark, for the Bowtie 2 presets parameter set:
```
./teaser.py example_ecoli.yaml --parameters bowtie2_presets
```

Example usage: Running the built-in E. coli example benchmark, only for BWA-MEM and BWA:
```
./teaser.py example_ecoli.yaml --mappers bwamem,bwa
```

#License
Teaser is made available under the MIT License.
