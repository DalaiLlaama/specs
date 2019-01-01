# Cleanup Protocol

![](./build/cleanup-protocol-state.png)

> NOTE: Notice that the `stale-invalid state` object has been removed from the previous figure shown in the [Uninstall Protocol](#uninstall-protocol) representing the effective "garbage collection" phenomena of the cleanup protocol

The cleanup protocol is a protocol that is periodically run to update the dependency of every active application to a newer root nonce version. In effect, it achieves the goal of O(1) constant time invalidation of outdated state put on-chain by resetting the state such that regardless of the number of historical / outdated apps that have been uninstalled, refuting their validitity on chain requires a single transaction.

## Messages

![](./build/cleanup-protocol-exchange.png)

> NOTE: The dependency in the message exchange is important; it is not safe to sign the root nonce commitment without possession of all the active app commitments.

### The **`CleanupInstall`** Message

| Field         | Description                      |
| ------------- | -------------------------------- |
| `protocol`    | `5`                              |
| `fromAddress` | The address of Alice             |
| `toAddress`   | The address of Bob               |
| `seq`         | `0`                              |
| `signature`   | Alice's signed commitment digest |

### The **`CleanupInstallAck`** Message

| Field         | Description                    |
| ------------- | ------------------------------ |
| `protocol`    | `5`                            |
| `fromAddress` | The address of Alice           |
| `toAddress`   | The address of Bob             |
| `seq`         | `1`                            |
| `signature`   | Bob's signed commitment digest |

## Commitments

**Commitments for `CleanupInstall` and `CleanupInstallAck`**:

For each active application, a similar commitment to the one described in the [Install Protocol](#install-protocol) must be generated. The commitment calls `executeAppConditionalTransaction` with a limit of `c_1 + c_2` and a expected root nonce key of `r + 1`. Note that this is different from the install commitment in that it is not a multisend and does not set the free balance. Note that the free balance is also considered an active app. Here is an example of a commitment for a given app:

![](./build/cleanup-protocol-commitment1.png)

Then, finally, the commitment update the root nonce is simply:

![](./build/cleanup-protocol-commitment2.png)