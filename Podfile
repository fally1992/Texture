source 'https://github.com/CocoaPods/Specs.git'

platform :ios, '9.0'

target :'AsyncDisplayKitTests' do
  pod 'OCMock', '=3.4.1' # 3.4.2 currently has issues.

  # TODO Move to Uber iOSSnapshotTestCase
  pod 'FBSnapshotTestCase/Core', :git => 'https://github.com/facebookarchive/ios-snapshot-test-case/', :tag => '2.1.4'
  
  pod 'JGMethodSwizzler', :git => 'https://github.com/JonasGessner/JGMethodSwizzler', :branch => 'master'

  # Only for buck build
  pod 'PINRemoteImage', '3.0.0-beta.13'
end

#TODO CocoaPods plugin instead?
post_install do |installer|
  require 'fileutils'

  # Assuming we're at the root dir
  buck_files_dir = 'buck-files'
  if File.directory?(buck_files_dir)
    installer.pod_targets.flat_map do |pod_target|
      pod_name = pod_target.pod_name
      # Copy the file at buck-files/BUCK_pod_name to Pods/pod_name/BUCK,
      # override existing file if needed
      buck_file = buck_files_dir + '/BUCK_' + pod_name
      if File.file?(buck_file)
        FileUtils.cp(buck_file, 'Pods/' + pod_name + '/BUCK', :preserve => false)
      end
    end
  end
end
