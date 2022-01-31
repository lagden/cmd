# Unix, OS X and Linux commands


## dscl (OS X)

Directory Service command line utility

#### Create a new entry in the local (/) domain under the category /users.
 - `dscl / -create /Users/lagden`

#### Create and set the shell property to bash.
 - `dscl / -create /Users/lagden UserShell /bin/bash`

#### Create and set the user’s full name.
 - `dscl / -create /Users/lagden RealName "Mr. Thiago Lagden"`

#### Create and set the user’s ID.
 - `dscl / -create /Users/lagden UniqueID 503`

#### Create and set the user’s group ID property.
 - `dscl / -create /Users/lagden PrimaryGroupID 1000`

#### Create and set the user home directory.
 - `dscl / -create /Users/lagden NFSHomeDirectory /Local/Users/lagden`

#### Set the password.
 - `dscl / -passwd /Users/lagden PASSWORD` or
 - `passwd lagden`

#### If you would like Mr. Lagden to be able to perform administrative functions:
 - `dscl / -append /Groups/admin GroupMembership lagden`

#### Add user to group
 - `sudo dseditgroup -o edit -a lagden -t lagden wheel`

#### Remove user from group
 - `sudo dseditgroup -o edit -d lagden -t lagden wheel`

#### List Group and Users
 - `dscacheutil -q group`


## Process and Kill

Process status and terminate or signal a process

#### Kill process by pattern
 - `pkill -x Google\ Chrome`

#### Kill process
 - `kill -9 1704`

#### Kill processes by name
 - `killAll Finder`

#### List process
 - `ps auxw`
 - you can combine: `ps auxw | grep Finder`


## nohup

Invoke a utility immune to hangups

#### Run Script in background and put output and stderror in log file
 - `nohup ./sample.sh > ./sample.log 2>&1 &`
 - `nohup ./import.sh > .import.log 2>&1 &`
 - `nohup php daemon/remote.php > /dev/null 2>&1 &`
 
[See atirax](https://github.com/lagden/atirax/blob/master/bin/atirax)


## ssh

OpenSSH SSH client

#### Generate a new SSH key.
 - `ssh-keygen -t rsa -C "youremail@youremail.com"`

#### export Display (It depends on the settings)

Enable X11 Forwarding with the `X11Forwarding yes` option set in `/private/etc/sshd_config`

 - ` ssh -XYC lagden@192.168.0.88`

#### usage Display

**Display On**

    export DISPLAY=IP:0.0
    xhost +


**Display Off**

    xhost -

    
## Find

Walk a file hierarchy

#### chmod recursive

**dirs**
    
    find ./ -type d -print0 |xargs -0 chmod 755

**files**

    find ./ -type f -print0 |xargs -0 chmod 644

#### find the files or directory and remove
 - `find . -name "arquivo.tar.*" -type f -ls -exec rm -f {} \;`
 - `find . -name "node_modules" -type d -exec rm -rf {} +`

#### find the files and compress
 - `find ./ -iname "*.conf" -type f -print0 | tar -czvf confs.tar.gz --null -T -`

## Tar

Manipulate tape archives

#### compress files tar gz
 - `tar cvzf foo.tgz *.cc *.h`

#### compress folder
 - `tar -zcvf folder.tar.gz /var/folder`

#### extract files tar gz
 - `tar xvzf foo.tgz`

#### extract files tar gz specific
 - `tar -zxvf bkp.tar.gz -C /home/lagden/projects/tmp/ bkp/*.sql`
 

## Misc

#### Symbolic link
 - `ln -s path/of/your/folder/or/file symbolic`

#### Socket sample
 - `telnet localhost 8526`

#### Watch (install the program before)
 - `watch -n 2 ls -al 20*`

#### Mount and Umount (SMB - OS X) 

    mkdir xxx
    mount_smbfs //user@server/folder ./xxx/
    umount ./xxx/

#### system Linux
 - `cat /proc/version`

#### system OS X
 - `sw_vers`
 - `system_profiler SPSoftwareDataType`
 
#### system
 - `uname -a`

#### Ubuntu version
 - `cat /etc/lsb-release`
 - `cat /etc/issue`

#### run remote command using bash script and ssh

    #!/bin/bash
    ssh user@host.com <<EOF
      nohup /path/to/run.sh > run.log &
    EOF
    echo 'done'
    exit 0

#### change MAC Address In Linux

    ifconfig eth0 down
    ifconfig eth0 hw ether 00:80:48:BA:d1:30
    ifconfig eth0 up
    ifconfig eth0 | grep HWaddr

#### change MAC Address In OS X

    ifconfig en1 | grep ether
    ifconfig en1 ether 00:e2:e3:e4:e5:e6

#### merge files

Copy directory hierarchies, create and extract archives

 - `ditto -V source destination`

#### rename regex sed
 - `ls _HistoriaPagina* | sed 's/\_HistoriaPagina\([0-9+]\).php/echo \1/' | sh`

#### rename using rename recursive

    find . -type f -name '*.sass' -exec rename -s jquery.mmenu. _ {} +
    find . -type f -name '*.scss' -ls -delete
    find . -type f -name 'jquery.mmenu.*' -ls -delete

#### curl ajax | jq (render readable json and required node)
 - `curl -H 'X-Requested-With: XMLHttpRequest' -d "my=var" http://192.168.1.250/ajax | jq '.'`
 
#### Find using grep
    
 - `grep -rnw ./directory -e "pattern"`
 - `grep --include=\*.{c,h} -rnw ./directory -e "pattern"`
 - `grep --exclude=*.o -rnw ./directory -e "pattern"`
 - `grep --exclude-dir={dir1,dir2,*.dst} -rnw ./directory -e "pattern"`

#### Permission _www to folder (OS X)
 - `sudo chmod -R +a "_www allow list,add_file,search,delete,add_subdirectory,delete_child,chown,file_inherit,di rectory_inherit" /Users/lagden/dev/apache`
 
#### Permission using ACL

    HTTPDUSER=`ps aux | grep -E '[a]pache|[h]ttpd|[_]www|[w]ww-data|[n]ginx' | grep -v root | head -1 | cut -d\  -f1`
    sudo setfacl -R -m u:"$HTTPDUSER":rwx -m u:lagden:rwx /my/super/folder
    sudo setfacl -dR -m u:"$HTTPDUSER":rwx -m u:lagden:rwx /my/super/folder
    
    sudo chmod 755 -R /my/super/folder
    sudo chmod g+s /my/super/folder
    sudo setfacl -d -m g::rwx /my/super/folder
    sudo setfacl -d -m o::rx /my/super/folder
    getfacl /my/super/folder

#### Redis

To have launchd start redis at login:

 - `ln -sfv /usr/local/opt/redis/*.plist ~/Library/LaunchAgents`

Then to load redis now:

 - `launchctl load ~/Library/LaunchAgents/homebrew.mxcl.redis.plist`

Or, if you don't want/need launchctl, you can just run:

 - `redis-server /usr/local/etc/redis.conf`

    
#### get folder git

`curl -fsSL https://github.com/lagden/example/archive/master.zip | tar -xz --strip-components=0 example-master`



#### Homebrew fix permission
 - sh: `sudo chown -R $(whoami):admin /usr/local`
 - fish: `sudo chown -R (whoami):admin /usr/local`


#### ffmpeg audio para zapzap e telegram

```
ffmpeg -i exemplo.m4a -c:a libopus audio.ogg
```
 
#### ffmpeg gif to mp4

```
ffmpeg -i /Users/lagden/Desktop/7EtVqiV.gif -c:v libx264 -pix_fmt yuv420p -movflags +faststart out.mp4
```

#### ffmpeg mov to gif

```
ffmpeg -t 30 -ss 0.5 -i in.mov -r "15" out.gif
```

or

```bash
#!/bin/sh

start_time=0.5
duration=30

palette="/tmp/palette.png"

filters="fps=15,scale=375:-1:flags=lanczos"

ffmpeg -ss $start_time -t $duration -i $1 -vf "$filters,palettegen" -y $palette
ffmpeg -ss $start_time -t $duration -i $1 -i $palette -lavfi "$filters [x]; [x][1:v] paletteuse" -y $2

exit
```

#### ffmpeg convert .mov to .mp4

```
ffmpeg -i videoName.mov -vcodec h264 -acodec mp2 videoName.mp4
ffmpeg -i videoName.mov -vcodec libx264 -pix_fmt yuv420p -profile:v baseline -level 3 videoName.mp4
```

#### ffmpeg convert .mov to .webm

```
ffmpeg -i videoName.mov -c:v libvpx -crf 10 -b:v 1M -c:a libvorbis videoName.webm
```

#### ffmpeg convert .mov to .ogg

```
ffmpeg -i videoName.mov -codec:v libtheora -qscale:v 7 -codec:a libvorbis -qscale:a 5 videoName.ogg
```

### DNS Flush

https://help.dreamhost.com/hc/en-us/articles/214981288-Flushing-your-DNS-cache-in-Mac-OS-X-and-Linux

### Ubuntu ini.d

```
start-stop-daemon --start --chuid mongodb --exec /usr/bin/mongod -- --config /etc/mongod.conf
```

### Process listening on a particular port

```
netstat -ltnp | ack-grep 3002

// output
tcp6       0      0 :::3002                 :::*                    LISTEN      1958/node
```

```
ps auxw | ack-grep 1958

// output
tex       1958  0.0  0.2 884208 33904 ?        Sl    2018   0:03 node /app/ramal/node_modules/.bin/micro -p 3002
```

## Copy to cliboard remote shell (OSX)

```
ssh user@10.0.1.123 "cat /etc/nginx/sites-enabled/site.conf" | pbcopy
```
