require "rosumi"
require "yaml"

CREDENTIALS_FILE = File.join(File.dirname(__FILE__), 'credentials.yml')
data = YAML.load_file(CREDENTIALS_FILE)
@@username = data['email']
@@password = data['password']
@@rosumi = Rosumi.new @@username, @@password

# Gets the device id and type for a login.
task :get_device_ids do

  devices = @@rosumi.devices

  if devices.nil? || devices.empty?
    puts "No devices found."
  end

  i=0
  while !devices[i].nil?
    device = devices[i]

    puts "---------- Device '#{i}' -------------"
    puts "Type: '#{device[:type]}'"
    puts "Name: '#{device[:name]}'"
    puts "-----------------------------------"
    puts "\n"
    
    i+=1
  end

end

task :locate_device, :id do |t, args|

  unless args[:id]
    puts "Please specify a device id."
    exit 1
  end 

  location = @@rosumi.locate_device(args[:id].to_i)

  puts "Could not get location for device #{args[:id]}." if location.nil?

  puts "---------- Device '#{args[:id]}' -------------"
  puts "Name: #{location[:name]}" unless location[:name].nil?
  puts "Coordinate: [#{location[:latitude]},#{location[:longitude]}]" unless location[:latitude].nil?
  puts "Accurracy: #{location[:accurracy]}" unless location[:accurracy].nil?
  puts "Timestamp: #{location[:timestamp]}" unless location[:timestamp].nil?
  puts "-----------------------------------"

end

task :message_device, :id, :subject, :message, :sound do |t, args|

  @@rosumi.send_message(args[:id].to_i, args[:subject], args[:message], args[:sound])
  puts "Message sent."

end
