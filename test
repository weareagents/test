#!/bin/bash
#######################################################################################################
#######################################################################################################
#######################################################################################################
######                                                                                          #######
######                                                                                          #######
######                 This script will help you to recover the accidentally                    #######
######                     deleted data from crashed linux file systems                         #######
######                                     Version-2                                            #######
######                          Script created by (Srijan Kishore)                              #######
######                                                                                          #######
######                                                                                          #######
#######################################################################################################                                                                                       
#######################################################################################################
#######################################################################################################


# User Check

if [ "$USER" = 'root' ]
    then

whiptail --title "User check" --msgbox "User is root, you can execute the script successfully." 8 78
             
        echo "User is root, you can execute the script successfully"
    else
whiptail --title "User check" --msgbox "User is not Root. Please run the script as root user." 8 78

        
        echo "User is not Root. Please run the script as root user."
        exit 1
fi


# Check your operating system

cat /etc/redhat-release >> /dev/null 
if [ "$?" = 0 ]
    then

whiptail --title "Your OS" --msgbox "You are using CentOS/Redhat/Fedora" 8 78
echo "You are using CentOS/Redhat/Fedora"

    else

whiptail --title "Your OS" --msgbox "You are not using CentOS/Redhat/Fedora.You can download the TestDisk from this link http://www.cgsecurity.org/wiki/TestDisk_Download" 8 78

    echo "You are not using CentOS/Redhat/Fedora.You can download the TestDisk from this link http://www.cgsecurity.org/wiki/TestDisk_Download"
    exit 1        
fi

#adding repo
ver=`cat /etc/redhat-release | cut -d " " -f3 | cut -d "." -f1`
ls -l /etc/yum.repos.d/rpmforge*

if [ "$?" != 0 ]
    
    then
    whiptail --title "Repository requirement" --msgbox "You need to add rpmforge repository to install testdisk" 8 78
        if [[ `uname -i` = 'i386' && $ver = 6 ]]
            then 
            echo "you are running i386 with 6 version"
            yum install -y http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.3-1.el6.rf.i686.rpm
        fi

        if [[ `uname -i` = 'x86_64' && $ver = 6 ]]
            then 
            echo "you are running i386 with 6 version"
            yum install -y http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.3-1.el6.rf.x86_64.rpm
        fi

        if [[ `uname -i` = 'i386' && $ver = 5 ]]
            then 
            echo "you are running i386 with 5 version"
            yum install -y http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.3-1.el5.rf.i386.rpm
        fi

        if [[ `uname -i` = 'x86_64' && $ver = 5 ]]
            then 
            echo "you are running x86_64 with 5 version"
            yum install -y http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.3-1.el5.rf.x86_64.rpm
        fi

        if [[ `uname -i` = 'x86_64' && $ver = 4 ]]
            then 
            echo "you are running i386 with 4 version"
            yum install -y http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.3-1.el4.rf.i386.rpm
        fi

        if [[ `uname -i` = 'x86_64' && $ver = 4 ]]
            then 
            echo "you are running x86_64 with 4 version"
            yum install -y http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.3-1.el4.rf.x86_64.rpm
        fi
else
whiptail --title "Repository requirement" --msgbox "You already have TestDisk repos configured" 8 78
echo "You already have TestDisk repos configured"
fi


# TestDisk installation
testdisk --version >> /dev/null
if [ "$?" = 0 ]
    then
    whiptail --title "Info" --msgbox "Testdisk already installed" 8 78
    echo "Testdisk already installed"
    else
    whiptail --title "Info" --msgbox "Testdisk not installed, installing Testdisk" 8 78
        echo "Testdisk not installed, installing Testdisk"

    yum install -y testdisk
fi
   

#Recovery part of deleted files


ls -l /root/result/lostfiles
if [ $? != 0 ]
    then
    mkdir -p /root/result/lostfiles
    whiptail --title "Data recovery" --msgbox "You are proceeding towards recovering the data from the lost drive. Please select the affected drive to get the data recovered" 8 78
    photorec /d /root/result/lostfiles

    else        
    whiptail --title "Folder Exists" --msgbox "There is already an existing folder viz /root/result/lostfiles, you are adviced to rename/remove the folder to allow the data recovery process" 8 78        
exit 2
fi

#File filtering
 
user=`ps aux | grep gnome-session | grep -v grep | head -1 | cut -d " " -f1`
mkdir "/home/recovered_output"
mkdir "/home/recovered_output/Debians"
mkdir "/home/recovered_output/rpms"
mkdir "/home/recovered_output/conf_files"
mkdir "/home/recovered_output/exe"
mkdir "/home/recovered_output/binaries"
mkdir "/home/recovered_output/Docs"
mkdir "/home/recovered_output/Pdfs"
mkdir "/home/recovered_output/Mbox"
mkdir "/home/recovered_output/Images"
mkdir "/home/recovered_output/Videos"
mkdir "/home/recovered_output/Sound"
mkdir "/home/recovered_output/ISO"
mkdir "/home/recovered_output/Excel"
mkdir "/home/recovered_output/Presentation"
mkdir "/home/recovered_output/Web_Files"
mkdir "/home/recovered_output/Archives"
mkdir "/home/recovered_output/Others"


#Sorting the Recovered data


find /root/result/ -name "*.doc"    -type f  -exec mv {} "/home/recovered_output/Docs/" \;
find /root/result/ -name "*.docx"   -type f  -exec mv {} "/home/recovered_output/Docs/" \;
find /root/result/ -name "*.odt"    -type f  -exec mv {} "/home/recovered_output/Docs/" \;
find /root/result/ -name "*.pdf"    -type f  -exec mv {} "/home/recovered_output/Pdfs/" \;
find /root/result/ -name "*.mbox"   -type f  -exec mv {} "/home/recovered_output/Mbox/"  \;
find /root/result/ -name "*.png"    -type f  -exec mv {} "/home/recovered_output/Images/" \;
find /root/result/ -name "*.jpg"    -type f  -exec mv {} "/home/recovered_output/Images/" \;
find /root/result/ -name "*.jpeg"   -type f  -exec mv {} "/home/recovered_output/Images/" \;
find /root/result/ -name "*.gif"    -type f  -exec mv {} "/home/recovered_output/Images/" \;
find /root/result/ -name "*.avi"    -type f  -exec mv {} "/home/recovered_output/Videos/" \;
find /root/result/ -name "*.mpeg"   -type f  -exec mv {} "/home/recovered_output/Videos/" \;
find /root/result/ -name "*.mp4"    -type f  -exec mv {} "/home/recovered_output/Videos/" \;
find /root/result/ -name "*.mkv"    -type f  -exec mv {} "/home/recovered_output/Videos/" \;
find /root/result/ -name "*.webm"   -type f  -exec mv {} "/home/recovered_output/Videos/" \;
find /root/result/ -name "*.wmv"    -type f  -exec mv {} "/home/recovered_output/Videos/" \;
find /root/result/ -name "*.flv"    -type f  -exec mv {} "/home/recovered_output/Videos/" \;
find /root/result/ -name "*.mp3"    -type f  -exec mv {} "/home/recovered_output/Sound/" \;
find /root/result/ -name "*.wav"    -type f  -exec mv {} "/home/recovered_output/Sound/" \;
find /root/result/ -name "*.deb"    -type f  -exec mv {} "/home/recovered_output/Debians/" \;
find /root/result/ -name "*.bin"    -type f  -exec mv {} "/home/recovered_output/binaries/" \;
find /root/result/ -name "*.exe"    -type f  -exec mv {} "/home/recovered_output/exe/" \;
find /root/result/ -name "*.rpm"    -type f  -exec mv {} "/home/recovered_output/rpms/" \;
find /root/result/ -name "*.conf"   -type f  -exec mv {} "/home/recovered_output/conf_files" \;
find /root/result/ -name "*.iso"    -type f  -exec mv {} "/home/recovered_output/ISO/" \;
find /root/result/ -name "*.xls"    -type f  -exec mv {} "/home/recovered_output/Excel/" \;
find /root/result/ -name "*.xlsx"   -type f  -exec mv {} "/home/recovered_output/Excel/" \;
find /root/result/ -name "*.csv"    -type f  -exec mv {} "/home/recovered_output/Excel/" \;
find /root/result/ -name "*.ods"    -type f  -exec mv {} "/home/recovered_output/Excel/" \;
find /root/result/ -name "*.ppt"    -type f  -exec mv {} "/home/recovered_output/Presentation/" \;
find /root/result/ -name "*.pptx"   -type f  -exec mv {} "/home/recovered_output/Presentation/" \;
find /root/result/ -name "*.odp"    -type f  -exec mv {} "/home/recovered_output/Presentation/" \;
find /root/result/ -name "*.html"   -type f  -exec mv {} "/home/recovered_output/Web_Files/" \;
find /root/result/ -name "*.htm"    -type f  -exec mv {} "/home/recovered_output/Web_Files/" \;
find /root/result/ -name "*.jsp"    -type f  -exec mv {} "/home/recovered_output/Web_Files/" \;
find /root/result/ -name "*.xml"    -type f  -exec mv {} "/home/recovered_output/Web_Files/" \;
find /root/result/ -name "*.css"    -type f  -exec mv {} "/home/recovered_output/Web_Files/" \;
find /root/result/ -name "*.js"     -type f  -exec mv {} "/home/recovered_output/Web_Files/" \;
find /root/result/ -name "*.zip"    -type f  -exec mv {} "/home/recovered_output/Archives/" \;
find /root/result/ -name "*.tar"    -type f  -exec mv {} "/home/recovered_output/Archives/" \;
find /root/result/ -name "*.rar"    -type f  -exec mv {} "/home/recovered_output/Archives/" \;
find /root/result/ -name "*.gzip"   -type f  -exec mv {} "/home/recovered_output/Archives/" \;
find /root/result/ -name "*.tar.gz" -type f  -exec mv {} "/home/recovered_output/Archives/" \;
find /root/result/ -name "*.7z"     -type f  -exec mv {} "/home/recovered_output/Archives/" \;
find /root/result/ -name "*.bz"     -type f  -exec mv {} "/home/recovered_output/Archives/" \;
find /root/result/ -name "*.bz2"    -type f  -exec mv {} "/home/recovered_output/Archives" \;
find /root/result/ -name "*.*"      -type f  -exec mv {} "/home/recovered_output/Others/" \;

#Finalization
whiptail --title "Congratulations" --msgbox "You have successfully recovered your data in folder /home/recovered_output cheers :)" 8 78
echo "You have successfully recovered your data in folder /home/recovered_output cheers :)"
exit 0
