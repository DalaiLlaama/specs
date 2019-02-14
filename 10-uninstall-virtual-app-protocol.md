# Uninstall Virtual App Protocol

This is the Uninstall Virtual App Protocol.

## Commitments

### lockCommitment

VirtualAppSetStateCommitment

### uninstallLeft

### uninstallRight

## Signatures

| Signature |   Commitment   | Signed By |
| --------- | -------------- | --------- |
| s1        | lockCommitment | A         |
| s2        | lockCommitment | I         |
| s3        | lockCommitment | B         |
| s4        | uninstallLeft  | A         |
| s5        | uninstallLeft  | I         |
| s6        | uninstallright | I         |
| s7        | uninstallright | B         |

## Messages

![](./build/uninstall-virtual-app-exchange.png)

| Message | Signatures |
| ------- | ---------- |
| m1      | s1         |
| m2      | s1, s2     |
| m3      | s3         |
| m4      | s2, s3     |
| m5      | s4         |
| m6      | s5         |
| m7      | s6         |
| m8      | s7         |
