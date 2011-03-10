# -*- ruby-*-

require 'ostruct'

desc "Install the application for this user"
task :install_user do
  ctoolu_install USER_DIRS
end

desc "Install the application for systemwide use"
task :install do
  ctoolu_install SYSTEM_DIRS
end

# FIXME, this is not exactly following 
# http://standards.freedesktop.org/basedir-spec/basedir-spec-latest.html
HOME = ENV['HOME']
USER_DIRS = {
  "bin" => "#{HOME}/bin",
  "xdg_config" => "#{HOME}/.config",
  "xdg_data" => "#{HOME}/.local/share",
}
SYSTEM_DIRS = {
  "bin" => "/usr/bin",
  "xdg_config" => "/etc/xdg",
  "xdg_data" => "/usr/share",
}

# calls FileUtils.install
# but assumes the target is a directory and ensures it exists
def dir_install(source, target_dir, options={})
  mkdir_p target_dir, options.merge({:mode => nil})
  install source, target_dir, options
end

# installs ctoolu, using a hash defining the base directories
def ctoolu_install(dirs)
  # make ostruct from hash for easier access
  dirs = OpenStruct.new(dirs) unless dirs.respond_to? :bin

  dir_install "ctoolu", dirs.bin, :mode => 0755
  dir_install "ctoolu.desktop", dirs.xdg_config + "/autostart"
  dir_install "actions.yaml", dirs.xdg_data + "/ctoolu"

  dir_install "clipboard-relay", dirs.bin, :mode => 0755
  dir_install "net.vidner.ClipboardRelay.service", dirs.xdg_data + "/dbus-1/services"
end
