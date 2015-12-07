##############################################################################
#                                    CNTK                                    #
##############################################################################

# 1. Documentation and Demos
-------------------------------

A detailed introduction to the Computational Network Toolkit (CNTK) and its
implementation as well as the user manual for CNTK can be found at

    "An Introduction to Computational Networks and the Computational
    Network Toolkit"

    by Amit Agarwal, Eldar Akchurin, Chris Basoglu, Guoguo Chen, Scott
    Cyphers, Jasha Droppo, Adam Eversole, Brian Guenter, Mark
    Hillebrand, Xuedong Huang, Zhiheng Huang, Vladimir Ivanov, Alexey
    Kamenev, Philipp Kranen, Oleksii Kuchaiev, Wolfgang Manousek,
    Avner May, Bhaskar Mitra, Olivier Nano, Gaizka Navarro, Alexey
    Orlov, Hari Parthasarathi, Baolin Peng, Marko Radmilac, Alexey
    Reznichenko, Frank Seide, Michael L. Seltzer, Malcolm Slaney,
    Andreas Stolcke, Huaming Wang, Kaisheng Yao, Dong Yu, Yu Zhang, and
    Geoffrey Zweig (in alphabetical order)

    Microsoft Technical Report MSR-TR-2014-112, 2014.

    Available through Codeplex and inside the repository.

To get started with examples see the Demos/ folder and the Readme therein.

There are also four files in the Documentation/ directory of the source 
that contain additional details.


# 2. Cloning the Source Code (Windows)
-------------------------------

The CNTK project uses Git as the source version control system.

If you have Visual Studio 2013 installed, Git is already
available. You can follow the "Clone a remote Git repository from a
third-party service" section under Set up Git on your dev machine
(configure, create, clone, add) and connect to
https://git01.codeplex.com/cntk to clone the source code. We found
that installing Git Extension for VS is still helpful esp. for new
users.

Otherwise you can install Git for your OS from the Using Git with
CodePlex page and clone the CNTK source code with the command

    git clone https://git01.codeplex.com/cntk


# 3. Cloning Source Code (Linux/Mac)
-------------------------------

Linux users should clone from this URL: https://git.codeplex.com/cntk

    git clone https://git.codeplex.com/cntk

More detail you can follow this thread: 
http://codeplex.codeplex.com/workitem/26133


# 4. Windows Visual Studio Setup (64-bit OS only)
-------------------------------

Install Visual Studio 2013. After installation make sure to
install Update 5 or higher: Go to menu Tools -> Extensions and
Updates -> Updates -> Product Updates -> Visual Studio 2013 Update 5
(or higher if applicable)

Install CUDA 7.0 from

    https://developer.nvidia.com/cuda-toolkit-70

and NVidia CUB from

    https://github.com/NVlabs/cub/archive/1.4.1.zip

by unzipping the archive and setting environment variable CUB_PATH to the location, e.g.:

    CUB_PATH=c:\src\cub-1.4.1

The easiest way to set a global environment variable is to press the windows
key, and then in the search interface start typing: edit environment
variables. Then close and reopen CMD shells and Visual Studio.

Install ACML 5.3.1 or above (specifically the ifort64_mp variant, e.g.,
acml5.3.1-ifort64.exe) from

    http://developer.amd.com/tools/cpu-development/amd-core-math-library-acml/acml-downloads-resources/

Before launching Visual Studio, set environment variable ACML_PATH, to
the folder you installed the library to, e.g.

    ACML_PATH=C:\AMD\acml5.3.1\ifort64_mp

If you are running on an Intel processor with FMA3 support, we also
advise to set ACML_FMA=0 in your environment to work around an issue in
the ACML library.

Alternatively if you have an MKL license, you can install Intel MKL
library instead of ACML from

    https://software.intel.com/en-us/intel-math-kernel-library-evaluation-options

and define USE_MKL in the CNTKMath project. MKL is faster and more
reliable on Intel chips if you have the license.

Install the latest Microsoft MS-MPI SDK and runtime from

    https://msdn.microsoft.com/en-us/library/bb524831(v=vs.85).aspx

If you want to use ImageReader, install OpenCV v3.0.0. Download and
install OpenCV v3.0.0 for Windows from

    http://opencv.org/downloads.html

Set environment variable OPENCV_PATH to the OpenCV build folder, e.g.

    C:\src\opencv\build

Make sure the following CUDA environment variables are set to the correct path

    CUDA_PATH=C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v7.0
    CUDA_PATH_V7_0=C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v7.0 
    
Open the CNTKSolution and build the CNTK project.

Note: If you make modifications to the code, please first disable the
insertion of TAB characters. If you use Visual Studio as your editor,
goto Tools|Options|Text Editor|C/C++|Tabs and make sure it is set to
Smart Indenting Tab, Indent Size set to 4, and "Insert Spaces" option
selected. You can also load the CppCntk.vssettings file (in the CNTK
home directory) which contains settings for C++ editor. To
import/export the settings, use Tools -> Import and Export
Settings... Visual Studio menu option.

Please do *not* auto-format existing code (Edit -> Advanced -> 
Format Document/Ctrl+E,D).


# 5. Linux GCC Setup
-------------------------------

Install needed libraries as indicated in the Windows section above on
your Linux box. You need GCC 4.8.4 or above.

Create a directory to build in and make a Config.make in the
directory that provides:

   * ACML_PATH= path to ACML library installation (only if MATHLIB=acml)

   * MKL_PATH= to MKL library installation (only if MATHLIB=mkl)

   * GDK_PATH= path to cuda gdk installation, such that
$(GDK_PATH)/include/nvidia/gdk/nvml.h exists (defaults to /usr)

   * BUILDTYPE= release (default) or debug

   * MATHLIB= acml (default) or mkl

   * CUDA_PATH= path to CUDA (if not specified, GPU will not be
enabled)

  * CUB_PATH= path to NVidia CUB installation, such that the
file $(CUB_PATH)/cub/cub.cuh exists (defaults to /usr/local/cub-1.4.1)

  * KALDI_PATH= Path to Kaldi (if not specified, Kaldi plugins will
not be built)

  * OPENCV_PATH= path to OpenCV 3.0.0 installation, such that the
directory $(OPENCV_PATH) exists (defaults to /usr/local/opencv-3.0.0)
 
Build the clean version using the following commands from the cntk folder

    mkdir -p build/release && cd build/release && ../../configure --with-buildtype=release

then 
    
    make -j all

Note: If you make modifications to the code, please first disable the
insertion of TAB characters in your editor.
