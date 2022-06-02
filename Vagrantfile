$install_script = <<-'SCRIPT'
# https://blog.amedama.jp/entry/ubuntu-1804-lts-sphinx-pdf-build
#wait `pgrep apt.systemd.dai`
PID=`pgrep apt.systemd.dai`
if [ -n "$PID" ]; then
  while [ -e /proc/$PID ]
  do
    sleep 1
  done
fi
sudo apt update
sudo apt -y install python3-pip python3-setuptools python3-wheel
sudo apt -y install texlive-latex-recommended texlive-latex-extra texlive-fonts-recommended texlive-fonts-extra texlive-lang-japanese texlive-lang-cjk latexmk
sudo pip3 install sphinx
sudo apt -y install texlive-full
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  # this box hanged up first time.
  # Once ran on VirtualBox,
  # "vagrant up also" worked.
  config.vm.hostname = "Sphinx"
  config.vm.boot_timeout = 6000

  config.vm.provider "virtualbox" do |v|
    v.name = "VagrantSphinx"
    v.cpus = 2
    # Memory in MB
    v.memory = 4096
  end

  config.vm.provision "shell", inline: $install_script
end
