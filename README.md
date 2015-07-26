# Puppet-aws-hiera


Usign hiera and puppet to launch aws instance

# install gems

$ sudo gem install hiera
$ sudo gem install hiera-puppet

# set hiera.yaml with content shwon below in /etc/puppetlabs/code/


:hierarchy:
  - common
:backends:
  - yaml


# create common.yaml file in /etc/puppetlabs/code/environments/production/hieradata/ with the following content

---
mi: ami-696e652c
region: eu-west-1
availability_zone: us-west-1a


#use hiera key-value 

ec2_instance { 'test':
  ensure          => present,
  image_id        => 'ami-a10897d6', 
   region         => hiera('region'), # use of  hiera
  instance_type   => 't2.micro',
  tags            => {
    department => 'dep',
    project    => 'pro',
    created_by => 'Joe',
  }
}





----etc
     |___puppetlaps
          |____ code (hiera.yaml )
                |_____environments
                      |____production
                           |__hieradata (common.yaml)
                      
                      
                      
