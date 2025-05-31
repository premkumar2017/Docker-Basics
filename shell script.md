🔹 File Operations
```bash
echo "1 2 3 ... 10"       # Print text to terminal
touch filename            # Create empty file
ls -ltr                   # List files by modification time (newest last)

🔹 Script Creation
bash
vi first_shell_script.sh  # Create/edit script with vi
vim second_shell_script.sh # Create/edit script with vim
cat first_shell_script.sh # Display script contents

🔹 Script Execution
bash
sh first_shell_script.sh  # Run script with sh interpreter
./first_shell_script.sh   # Execute directly (requires +x permissions)
chmod +x script.sh       # Make script executable

🔹 Shebang Headers
bash
#!/bin/bash    # Bash interpreter
#!/bin/sh     # POSIX-compliant shell
#!/bin/ksh     # Korn shell
#!/bin/dash    # Debian Almquist shell
🔹 Help & Documentation
bash
man touch      # Show manual for touch command
echo "My name is $(whoami)"  # Dynamic output example
