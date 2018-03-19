# Google Colaboratory (Free GPU) Guide

Using GPU seems to be necessary to train model (especially deep learning model), but installing my own GPU requires money and annoying process.. Google has a free cloud service which support FREE GPU service. 

This material is created based on the medium blog([Here](https://medium.com/deep-learning-turkey/google-colab-free-gpu-tutorial-e113627b9f5d)), which is an awesome and easy posting about hot to use google colab. Please reade the posting.

This github page summarize the posting to help others (including me) to start to use Google colab.

1. Create Folder on Google Drive. Here, I set the folder's name as "app" (You can set any as a folder's name)

    Click <b>New</b> (Top left) > <b>Folder</b>

2. Create Jupyter Notebook File via

    <b>Right click</b>  > <b>More</b>  > <b>Colaboratory</b> 
    
3. <b>Setting Free GPU</b>

    <b>Edit</b>  > <b>Notebook setting</b>  
    
        Runtime type (either Python 2 or Python 3)
        Hardware accelerator > GPU
        

4. Check whether GPU is working? '/device:GPU:0' should be printed with this comments

        import tensorflow as tf
        tf.test.gpu_device_name()
        
        
5. Done!! Let's use Google Colab.


## Wait, import libraries doesn't work! Run these codes first to install the necessary libraries and perform authorization.
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
 
 1. Directory name is: "drive/app/directory_name"
 
 2. Changing working directory :
 
          import os
          os.chdir("drive/app")
