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

raw_tx = File.opne('spec/bitcoin/fixtures/rawtx-01.bin', 'rb') {|f| f.read }
rx = Bitcoin::Protocol::Tx.new(raw_tx)
tx.hash 
tx.in.size 
tx.out.size
tx.to_hash
Bitcoin::Protocol::Tx.from_json( tx.to_json )
Bitcoin::Script.new(tx.out[0].pk_script).to_string

rawtx1 = File.open("spec/bitcoin/fixtures/rawtx-xxxxxxx.bin", 'rb') {|f| f.read}
rawtx2 = File.open("spec/bitcoin/fixtures/rawtx-xxxxx.bin", 'rb') {|f| f.read}
tx1 = Bitcoin::Protocol::Tx.new(rawtx1)
tx2 = Bitcoin::Protocol::Tx.new(rawtx2)

tx1.verify_input_signature(0, tx2)

txin = tx1.in.first
txout = tx2.out[txin.prev_out_index]
script = Bitcoin::Script.new(txin.script_sig + txout.pk_script)

result = script.run do |pubkey, sig, hash_type|
  hash = tx1.signature_hash_for_input(0, nil, txout.pk_script)
  Bitcoin.verify_signature(hash, sig, pubkey.unpack("H*")[0])
end
result

Bitcoin.network = :testnet3
include Bitcoin::Builder
prev_hash = "xxx"
prev_out_index = 0
prev_tx = Bitcoin::P::Tx.from_json(open("http://test.webbtc.com/tx/#{prev_hash}.json"))
key = Bitcoin::P::Tx.from_json(open("http://test.webbtc.com/tx/#{pre_hash}.json"))
key = Bitcoin::Key.from_base58("xxxx")
new_tx = build_tx do |t|

  t.input do |i|
    i.prev_out prev_tx
    i.prev_out_index prev_out_index
    i.signature_key key
  end
  
  t.output do |o|
    o.value 50000000
    o.script {|s| s.recipient "xxx"}
  end
  
  t.output do |o|
    o.value 49000000
    o.script {|s| s.recipient key.addr }
  end
end

puts new_tx.to_json
```

```sh
gem install bitcoin-ruby
git clone https://github.com/lian/bitcoin-ruby.git; cd bitcoin-ruby; bundle install

rake doc
rake build_libsecp256k1
rake rspec
bundle exec rspec spec/bitcoin/bitcoin_spec.rb
rake coin_spec[dogecoin]
```

