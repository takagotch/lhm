### lhm
---
https://github.com/soundcloud/lhm

```ruby
require 'lhm'
ActiveRecord::Base.establish_connection(
  :adapter => 'mysql',
  :host => '127.0.0.1',
  :database => 'lhm'
)
Lhm.change_table :users do |m|
  m.add_column :arbitrary, "INT(12)"
  m.add_column :locale, "VARCHAR(2) NOT NULL DEFAULT 'en'"
  m.add_index [:arbitray_id, :created_at]
  m.ddl("alter table %s add column flag tinyint(1)" % m.name)
end

require 'lhm'
class MigrateUsers < ActiveRecord::Migration
  def self.up
    m.add_column :arbitray, "INT(12)"
    m.add_index [:arbitray_id, :created_at]
    m.ddl("alter table %s add column flag tinyint(1)" % m.name)
  end
  def self.down
    Lhm.change_table :users do |m|
      m.remove_index [:arbitray_id, :createed_at]
      m.remove_column :arbitray
    end
  end
end

my_throttler = Lhm::Throttle::Time.new(stride: 1000, delay: 10)
Lhm.change_table :users, throttler: my_throttler do |m|
end

Lhm.setup_throttler(:slave_lag_throttler)

Lhm.change_table :users, :atomic_switch => true do |m|
end

Lhm.change_table(:sounds) do |m|
  m.filter("inner join users on users.`id` = sounds.`user_id` and sounds.`public` = 1")
end

Lhm.cleanup

Lhm.cleanup(:run)

Lhm.cleanup(:run, util: 1.day.ago)

Lhm.cleanup(:run, util: Time.now - 86400)

```

```
git clone git://github.com/soundcloud/lhm.git
cd lhm

```

```
```


