# homeserver
Steps to setup home server

## Create Server

Get Ubuntu Server 22.04 from https://ubuntu.com/download/server

<ul>
  <li>Install Ubuntu Server 22.04
  <li>Make sure to enable SSH server
</ul>

## Update

sudo apt update && sudo apt upgrade -y

## Ensure hardware able to use virtualization

<ul>
  <li>sudo apt install -y cpu-checker
  <li>kvm-ok
</ul>

## Install Graphical User Interface

<ul>
  <li>sudo ubuntu-drivers autoinstall
  <li>sudo apt install -y ubuntu-desktop-minimal firefox
  <li>sudo systemctl set-default graphical
  <li>sudo reboot now
</ul>

## Install Virtual Manager

<ul>
  <li>sudo apt install -y qemu-kvm virt-manager libvirt-daemon-system virtinst libvirt-clients bridge-utils
  <li>sudo systemctl enable --now libvirtd
  <li>sudo systemctl start libvirtd
</ul>

## Configure Virtual Networking

<ul>
  <li>sudo nano /etc/systemd/network/br.netdev

  [NetDev]
  Name=br0
  Kind=bridge

  <li>sudo nano 1-br0-bind.network

  [Match]
  Name=eno1

  [Network]
  Bridge=br0

<li>sudo nano /etc/systemd/network/2-br0-dhcp.network

  [Match]
  Name=br0

  [Network]
  DHCP=ipv4

<li>systemctl enable systemd-networkd

<li>sudo reboot now
</ul>
