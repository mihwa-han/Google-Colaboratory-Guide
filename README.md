# Google Colaboratory (Free GPU) Guide

Using GPU processing power seems to be necessary to train many machine learning models (especially deep learning models), but installing your own GPU requires money and it's often an annoying process. Google has a free cloud service which support FREE GPU cloud computing resources. 

This guide is based on the Medium blog ([Here](https://medium.com/deep-learning-turkey/google-colab-free-gpu-tutorial-e113627b9f5d)), which is an awesome and easy-to-follow posting about how to use Google Colab. Please read the article for a detailed introduction.

This GitHub page summarizes the blog post to help others (including me) to get started using Google Colab.

1. Create Folder on your [Google Drive](https://www.google.com/drive/). Here, I set the folder's name as "app" (You can choose whatever name you like, of course)

    Click <b>New</b> (Top left) > <b>Folder</b>

2. Create Colaboratory (Notebook) File via

    <b>Right click</b>  > <b>More</b>  > <b>Colaboratory</b> 
    
3. <b>Setting Free GPU</b>

    <b>Edit</b>  > <b>Notebook setting</b>  
    
        Runtime type (either Python 2 or Python 3)
        Hardware accelerator > GPU
        

4. Check whether GPU is working? If you enter the following text into a cell: 

        import tensorflow as tf
        tf.test.gpu_device_name()
        
    You should see the following output: '/device:GPU:0'.
        
5. Done!! Let's use Google Colab.


## Wait, importing Python libraries doesn't work! Run these codes first to install the necessary libraries and perform authorization.
1. Run the scripts below:

        !apt-get install -y -qq software-properties-common python-software-properties module-init-tools
        !add-apt-repository -y ppa:alessandro-strada/ppa 2>&1 > /dev/null
        !apt-get update -qq 2>&1 > /dev/null
        !apt-get -y install -qq google-drive-ocamlfuse fuse
        from google.colab import auth
        auth.authenticate_user()
        from oauth2client.client import GoogleCredentials
        creds = GoogleCredentials.get_application_default()
        import getpass
        !google-drive-ocamlfuse -headless -id={creds.client_id} -secret={creds.client_secret} < /dev/null 2>&1 | grep URL
        vcode = getpass.getpass()
        !echo {vcode} | google-drive-ocamlfuse -headless -id={creds.client_id} -secret={creds.client_secret}

2. When you run the code, you can see "Go to the following link in your browser:"
<b>Click</b>  the link and <b>copy</b> verificiation code and <b>paste</b> it to text box with "Enter verification code:"

3. Mount your Google Drive:

        !mkdir -p drive
        !google-drive-ocamlfuse drive
        
4. Finally, you can install what you want. For example, if you want to install Keras:

        !pip install -q keras
        
        
 ### Useful Tips
 
 1. Default directory is: "drive/app/directory_name"
 
 2. To change your working directory:
 
          import os
          os.chdir("drive/app")
