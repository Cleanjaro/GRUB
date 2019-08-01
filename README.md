<p>A Clean version of grub for Manjaro, removing all silent boot patches. Restoring grub back to its standard operation.</p>
<p>You can also add the following repository to your pacman.conf file for automatic updates.</p>
<p>[cleanjaro]<br>
SigLevel = Optional TrustAll<br>
Server = <a href="https://majinbuu.com/cleanjaro/">https://majinbuu.com/cleanjaro/</a></p>
<p>To install run:<br>
sudo pacman -Syu grub-clean</p>
