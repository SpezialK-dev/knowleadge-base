# Knowen problems 
Sway currently has problems with lightDM -> if you use LightDM it just will not start. 

# Some pluggins 

[wiki](https://github.com/swaywm/sway/wiki/Useful-add-ons-for-sway)


# Java Gui applications 

if you have java applications that are writen with the normal java application framework, you might encounter the application starting but the thing just staying white. 
In that case add the following line to your bashrc and exit sway and reload the bash config. 
```bash
export _JAVA_AWT_WM_NONREPARENTING=1
```

After that the application should no longer stay white 
