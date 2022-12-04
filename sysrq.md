## https://askubuntu.com/questions/11002/alt-sysrq-reisub-doesnt-reboot-my-laptop/334292#334292

## in debian, SysRqs are normally masked and partially disabled.
cat /proc/sys/kernel/sysrq 

## to enable
echo "1">/proc/sys/kernel/sysrq

You press the key combo Alt + SysRq + command key (REISUB).
