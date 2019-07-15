### bitcoin-ruby
---
https://github.com/lian/bitcoin-ruby

```rb
key = Bitcoin::Key.generate
key.priv
key.pub
key.addr
sig = key.sign("data")
key.verify("data", sig)
recovered_key = Bitcoin::Key.from_base58(key.to_base58)

gem 'bitcoin-ruby', git: 'https://github.com/lian/bitcoin-ruby', branch: 'master', require: 'bitcoin'

raw_block = File.open('spec/bitcoin/fixtures/rawblock-0.bin', 'rb') {|f| f.read}
blk = Bitcoin::Protocol::Block.new(raw_block)
blk.hash
blk.tx.count
blk.to_hash
Bitcoin::Protocol::Block.from_json( blk.to_json )

```

```sh
gem install bitcoin-ruby
git clone https://github.com/lian/bitcoin-ruby.git; cd bitcoin-ruby; bundle install
```

