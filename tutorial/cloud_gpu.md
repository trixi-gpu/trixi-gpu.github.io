# Setup a Cloud GPU for Running CUDA.jl

This tutorial will guide you through setting up a cloud GPU for running CUDA.jl. Since the author is familiar with the AWS cloud platform, we use it as our example for illustration. The process is similar across other cloud platforms when launching a cloud GPU, and we hope this guidance will help.

## Prerequisites

Before starting the tutorial, you'll need to launch a P-type EC2 instance in AWS. Below are some key resources to help you understand the basics and successfully launch your instance:

- [What is Amazon EC2?](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html) – Learn the core concepts of Amazon EC2.
- [Which type of EC2 should I use?](https://aws.amazon.com/ec2/instance-types/) – Discover the best EC2 instance types for your workload.
- [How to launch Amazon EC2?](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html) – Step-by-step guide on launching your first EC2 instance.
- [What is a Spot Instance?](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-spot-instances.html) *(optional)* – Learn about spot instances for cost savings.
- [How to work with Spot Instances?](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/spot-requests.html) *(optional)* – Guide on using spot instances effectively.

If cost is not a concern, you can opt for on-demand instances and skip the last two resources. However, in both cases, you'll need to manually request a quota for P-type instances before launching.

## Connect to Instance

Up to this point, we assume you have already launched your EC2 instance. Now, it's time to connect to your instance using your local terminal or any IDE with SSH extension support.

First, move your `.pem` key pair file to your `.ssh` folder for better security and convenience:
```bash
$ mv ~/Downloads/<your-key-pair-name>.pem ~/.ssh/<your-key-pair-name>.pem
```

To prevent any permission issues when connecting, set the appropriate permissions on the key pair file:
```Bash
$ chmod 600 ~/.ssh/<your-key-pair-name>.pem
```

Copy the public IPv4 DNS of your instance from the AWS console, then connect using the SSH command below:
```Bash
$ ssh -i ~/.ssh/<your-key-pair-name>.pem ubuntu@<your-ec2-public-ipv4-dns>
```

When prompted with the message `Are you sure you want to continue connecting (yes/no)?`, type `yes` to proceed. After confirming, you should successfully connect to your EC2 instance.

## Configure CUDA Toolkit

You can then proceed to download and configure the appropriate version of the CUDA Toolkit for your platform. Visit [NVIDIA CUDA Downloads](https://developer.nvidia.com/cuda-downloads) to find the specific commands for your platform.

Once the installation is complete, verify that the CUDA Toolkit is properly installed by running the following command:
```bash
$ nvcc --version
```
This will confirm the installed CUDA version.

## Configure Julia Package

To install Julia, first visit [Julia Downloads](https://julialang.org/downloads/) and select the version you need. For this example, we will use Julia version 1.10.0 for Linux on x86 64-bit.

Copy the download link for the selected Julia version and use the following command to download it to your instance:
```bash
$ wget https://julialang-s3.julialang.org/bin/linux/x64/1.10/julia-1.10.0-linux-x86_64.tar.gz
```

Once downloaded, extract the contents of the package:
```bash
$ tar -xvf julia-1.10.0-linux-x86_64.tar.gz
```

To make Julia easily accessible from anywhere, create a symbolic link to the Julia binary:
```bash
$ sudo ln -s ~/julia-1.10.0/bin/julia /usr/local/bin/julia
```

You can delete the original `.tar.gz` file to save space if needed:
```bash
$ rm julia-1.10.0-linux-x86_64.tar.gz
```

Finally, run the following command to ensure Julia is installed and accessible:
```bash
$ julia
```

## Add the CUDA.jl to Julia

In this step, we will add the CUDA package (i.e., [CUDA.jl](https://cuda.juliagpu.org/stable/)) to Julia for GPU programming. Before proceeding, ensure that you are already connected to your instance.

Enter the Julia REPL by typing `julia` in the terminal. Once inside, add the CUDA.jl using the following commands:
```julia
julia> using Pkg
julia> Pkg.add("CUDA")
```

To ensure that CUDA.jl is installed and working correctly, run the following commands in the Julia REPL:
```julia
julia> using CUDA
julia> CUDA.versioninfo()
```
If the version information is displayed without any errors, you've successfully added CUDA.jl to Julia, and it is ready for use.

## Enable SSH with Git Repository (Optional)

This step is optional but recommended if you plan to operate a Git repository on your EC2 instance.

In your local terminal, generate an SSH key with the following command:
```bash
$ ssh-keygen -t rsa -b 4096 -C "<your-email-address>"
```
Save the key to the default directory (`~/.ssh`) and choose a passphrase for added security. Remember to change 
the permissions of your SSH private key to ensure it's secure:
```bash
$ chmod 600 ~/.ssh/id_rsa
```

Add the private key to the SSH agent to allow SSH connections:
```bash
$ ssh-add -k ~/.ssh/id_rsa
```

Copy the public SSH key from your machine and add it to your GitHub account:
```bash
$ cat ~/.ssh/id_rsa.pub
```
Follow [GitHub's guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) to create a new SSH key in GitHub using the output and then
transfer your public key to the `authorized_keys` file on your EC2 instance:
```bash
$ cat ~/.ssh/id_rsa.pub | ssh -i ~/.ssh/<your-key-pair-name>.pem ubuntu@<your-ec2-public-ipv4-dns> "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

Finally, copy your private SSH key to your EC2 instance for Git operations:
```bash
$ scp -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no -i ~/.ssh/<your-key-pair-name>.pem ~/.ssh/id_rsa ubuntu@<your-ec2-public-ipv4-dns>:~/.ssh/
```
You can now perform Git operations, such as `git clone` and `git push`, directly from your EC2 instance.

## End

After going through the previous steps, you can use CUDA.jl on your cloud GPU through AWS. Please remember to stop your instance when you're not using it and terminate it when you no longer need it, as both of them will incur extra charges.