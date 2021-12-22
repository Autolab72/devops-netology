
Какие ресурсы выделены по-умолчанию?

- 1GB RAM, 2 CPU(100% load),  VRAM 4Mb(хотя виртуалбокс пишет что минимум 9Мб), VMDK 64GB

Как добавить оперативной памяти или ресурсов процессора виртуальной машине?

config.vm.provider "virtualbox" do |v|
  v.memory = 1024
  v.cpus = 2
  v.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
end


  
