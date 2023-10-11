# Uncomment the next line to define a global platform for your project
# platform :ios, '9.0'
platform :ios, '14.0'
plugin 'cocoapods-pod-linkage'

source 'https://github.com/CocoaPods/Specs.git'

inhibit_all_warnings!
install! 'cocoapods',
         :disable_input_output_paths => true,
         :warn_for_unused_master_specs_repo => false
use_frameworks! :linkage => :static

target 'HappyRoll' do
  # 基础大仓库
  pod 'Storehouse', :path => '../../FlyBaseStore/Storehouse/'
  
  # Pods for HappyRoll
  pod 'GRDB.swift'
  pod 'R.swift'
  pod 'lottie-ios','3.5' , :linkage => :dynamic # 包含IBDesignable不能是静态库
  pod 'IBAnimatable', :linkage => :dynamic # 包含IBDesignable不能是静态库
  # Swift_IconFont
    
  target 'HappyRollTests' do
    inherit! :search_paths
    # Pods for testing
  end

  target 'HappyRollUITests' do
    # Pods for testing
  end

end

post_install do |installer|
  # 消除IPHONEOS_DEPLOYMENT_TARGET告警
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      if config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'].to_f < 11.0
        config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = '11.0'
      end
    end # target.build_configurations.each
  end # installer.pods_project.targets.each
  # 清除XIB告警
  installer.pods_project.build_configurations.each do |config|
    next unless config.name == 'Debug' || config.name == 'DebugProfile'
    config.build_settings['LD_RUNPATH_SEARCH_PATHS'] = [
      '$(FRAMEWORK_SEARCH_PATHS)'
    ]
  end
  # 解决iOS16签名不一致问题
  installer.generated_projects.each do |project|
    project.targets.each do |target|
        target.build_configurations.each do |config|
            config.build_settings['CODE_SIGN_IDENTITY'] = ''
         end
    end
  end
  # 解决Xcode14编译产物加载不到swiftCoreGraphics的问题
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      if config.build_settings['OTHER_LDFLAGS'] != nil
        config.build_settings['OTHER_LDFLAGS'] += ' -weak-lswiftCoreGraphics'
      else
        config.build_settings['OTHER_LDFLAGS'] = '$(inherited)  -weak-lswiftCoreGraphics'
      end
    end
  end
end
