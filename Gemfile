source "https://rubygems.org"

gem "cocoapods"
gem "cocoapods-pod-linkage"
gem "xcodeproj"
gem "fastlane"

# Sonar集成
# gem install slather
# gem install tailor
# gem install xcpretty
# Sonar其他依赖
# xcodebuild
# brew install swiftlint
# brew tap oclint/formulae && brew install oclint
# brew install sonar-scanner
# pip3 install lizard

plugins_path = File.join(File.dirname(__FILE__), 'fastlane', 'Pluginfile')
eval_gemfile(plugins_path) if File.exist?(plugins_path)
