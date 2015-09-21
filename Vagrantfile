options = {}
options['virtualbox_network_name'] = "VIRTUALBOX_NETWORK_NAME"
nodes = {
  "cloudferryBUILD_NAME" => {
    "box" => "hashicorp/precise64",
    "ip" => "192.168.1.2",
    "memory" => 1536,
    "cpus" => 1,
    "role" => "lab"
 }
}
Vagrant.configure(2) do |config|
  nodes.each do |nodename, nodedata|
    config.vm.define nodename do |thisnode|
      thisnode.vm.box = nodedata['box']
      thisnode.vm.hostname = nodename
      if nodedata.has_key?("ip") then
        thisnode.vm.network "private_network", ip: nodedata['ip'],
          virtualbox__intnet: options['virtualbox_network_name']
      end
      
      thisnode.vm.provider "virtualbox" do |v|
        v.memory = nodedata.fetch("memory", 1024)
        v.cpus = nodedata.fetch("cpus", 2)
        v.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
        v.customize ["modifyvm", :id, "--cpuexecutioncap", "80"]
      end
    end
  end
end
