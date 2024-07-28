# Benchmark Groth16 Circom Circuits
Require: rapidsnark

1. Set `.env` file: ptau and rapidsnark
2. Compile the circuits and Benchmark
```sh
./1-prepare.sh

./2-benchmark.sh rsa rsa
./2-benchmark.sh keccak256 keccak256

for size in {100k,400k,1200k,1600k,3200k}
do
    ./2-benchmark.sh complex-circuit complex-circuit-$size-$size
    sleep 0.1
done
```

# Benchmarking Results for Email-wallet by [ZK-Email](https://github.com/zk-email)
## email-sender.circom
- This is the largest circuit we have so far with close to `2M` constraints.
- I had considered the Sample Size to be `10` for calculating average time for proving and verifying.
- `tachyon` is around `35%` faster than `rapidsnark` in the `proving time`.
- `tachyon` has used `mmap` [see this PR](https://github.com/kroma-network/tachyon/pull/490) to speed up the `zk key parsing` and `witness parsing`.
![alt text](<email_sender_benchmark.png>)

## announcement.circom
![alt text](<announcement_benchmark.png>)

## claim.circom
![alt text](<claim_benchmark.png>)


## Credits
Scripts from https://github.com/zkmopro/mopro