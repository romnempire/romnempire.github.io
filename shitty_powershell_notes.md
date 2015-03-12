---
title: shitty powershell notes
layout: post
---

#11 March 2015 creating a shitty script to run ssh-agent on startup

##Notes

TURN OFF POWERSHELL SECURITY MECHANISM FOR SIGNED SCRIPTS ONLY
     THIS SHOULD TURN IT OFF PERMANENTLY
     THIS SETTING IS DIFFERENT BETWEEN THE X86 AND X64 POWERSHELLS

THERE IS A POWERSHELL LIBRARY CALLED THE PSSCHEDULEDJOB MODULE THAT AUTOMATES MAKING TASK SCHEDULER TASKS IN POWERSHELL.  DON'T USE THIS

there's also one for 'tasks' that comes fro windows 8 idk about it either.

ANYWAYS IF YOU DO IT you WILL need to fuck wit the task scheduler anyways

WHY?  BECAUSE YOU'RE ON A LAPTOP AND ONE OF THE DEFAULT TASK SCHEDULER SETTINGS IS DON'T RUN ON BATTERY POWER.  WHICH YOU WANT, AND CAN ONLY SET IN TASK SHEDULER (I THINK but i didin't look hard)

IN THE TECHNET LIBRARY THERE IS A https://technet.microsoft.com/en-us/library/bb978526.aspx THIS IS THE OFFICIAL DOCS I THINK IT HAS EVERYTHING.  A LOT OF IT IS HIDDEN IN THE ABOUT_MODULE PAGES THOUGH.  LEARN TO READ IT

OKAY SO YOU'VE OPENED THE TASK SCHEDULER AND YOU WANT TO MAKE AA TASK.  DON'T TRY TO RUN TASKS AS ADMINISTRATOR, BECAUSE BY DEFAULT ADMINISTRATOR HAS A HIDDNE PASWORD FOR SECUIRTY.  INSTEAD USE 'HIGHEST PRIVILEGE'.  BUT THAT'S NOT IMPORTANT HERE.  

YOU MIGHT GET A fffd0000 powershell ERROR.  THIS CAN MEAN YOU'RE TRYING TO STUFF YOU DON'T HAVE PRIVILEGES FOR, IT CAN ALSO MEAN YOU WROTE SOMETHING WRONG IN THE TASK SETUP.

WHEN DEBUGGING A PS SCRIPT AS A TASK, THE PROBLEM IS POWERSHELL DOES DIFFERENT THINGS WHEN YOU'RE IN AN INTERACTIE SHELL AND WHEN YOU'RE RUNNING A SCRIPT.  SO YOURE GOING TO HAVE TO RUN IT AS A SCRIPT FROM THE DROPDOWN, AND THAT'S GOING TO FLASH ERROR MESSAGES.  YOU HAVE ACCESS TO A THREAD WAIT FUNCTION

THEN TRY TO DEBUG THE TASK.  WHEN YOU RUN A TASK MANUALLY FROM THE TSK SCHEDULER IT'S NOT GUARANTEED TO UPDATE FAST OR AT ALL, SO JUST CLOSE OUT AND THEN RESTART THE GUI.  YOU MAY ALSO WANT TO WRITE TO A LOG FILE JUST BECAUSE THIS IS NONDETERMINISTIC.

THEN TRY TO DEBUG THE TRIGGER.

SO WHEN YOU RUN A PRROCESS THROUGH THE TASK SCHEUDLER, IT SEEMS TO BE RUNNING IT OUT OF USER SPACE.  WHEN YOU GO INTO TASK MANAGER, IT WILL BE HIDDEN UNDER SHOW PROCESSES FOR ALL USERS.

THIS IS BAD BECAUSE IT PUTS THE ENVIRONMENT VARIABLES IN THE WRONG USERSPACE, WHICH IS EITHER INACCESSIBLE OR YOU COULD STICK IT IN GLOBAL WICH SOUNDS LIKE A BAD IDEA

also use rapid environemnt editor to view current state of environment variables because shells don't seem to always update.

BUT MORE IMORTANTLY if ssh-agent is in admin space, ssh-add won't access it.  this is probably a reasonable security precaution...

when run with escalated permissions, Administrator is making processes with process owner Roman, which hides them ehind the show all processes bar

but we need escalated permissions because without them the script is terminating processes?

THE PROBLEM IS IT'S RUNNING IT OUTSIDE OF USERSPACE, WHICH MAKES IT SET THE WRONG ENVIRONMENT VARIABLES AND MAKES SSH-ADD UNABLE TO ACCESS IT, EVEN WITHOUT ESCALTED PERMISSIONS

but when we do this, the environment variables we set are in the wrong userspace, and putin g them in system is a risk...

##Context

so like you know how it sucks to git really hard and then have to type in your password every time on windows?  well, this would all be solved if i didn't use windows or soemthing.  anyways so you gotta run an authentication agent at startup and for some godforsaken reason nobody seems to have done it and posted it on the internet.  Maybe because you should jsut use msysgit or use putty's daemon to authenticate but whatever.  I DECIDED TO ACCEPT THE CHALLENGE and get ssh-agent to run on logon in windows.

so the problem is that you can't just run ssh-agent.  You have to 

* run ssh-agent
* eval ssh-agent's stdout stream to populate some enviornment variables
* run ssh-add to add keys and secret passcodey things (which looks at the envs)

note the eval thing means gg if you're windowsing.  but I could just cygwin, rite?  Nope, because you have to populate the envs in userspace if you want to be able to run git push on the Command Line.  (why not just always run the git mingw bash instead of the command line?  look i think i already established there are easier alternatives and I AM ACCEPTING A CHALLENGE HERE.

anyways, i started out in windows shell script and realized regexes would make parsing the stdout stream easier so i was like lets do it in powershell.  after tons of mishaps i kept not taking the easy way out to do it in THE OFFICIAL POWERSHELL WAY.  like, after i got the script running, i could have just added it to the startup folder (except windows doesn't execute ps1 scripts as a default behaviour so i would have had to have added a batch script that called the powershell script because 'security' or something)  so i dicked around withthe PSSCHEDULEDJOB module, and then directly with the task scheduler gui when that didn't work as intented.

##Resolution

so as it turns out, the task scheduler runs processes in a different user space or something which dicks up ssh-add and also the ability to set envs.  I finally FALED THE CHALLENGE OF DOING IT THE POWERSHELL WAY and said fuck it i'll do it in python.  Minutes later I had it running, if you want the script [here's a gist](https://gist.github.com/romnempire/290b6bc10841a1d8aba5).
