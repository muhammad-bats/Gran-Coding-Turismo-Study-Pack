# Example Problem 5: Loose Change

## Problem Statement
At a lemonade stand, each lemonade costs `$5`. Customers are standing in a queue to buy from you and order one at a time (in the order specified by `bills`). Each customer will only buy one lemonade and pay with either a `$5`, `$10`, or `$20` bill. You must provide the correct change to each customer so that the net transaction is that the customer pays `$5`.

**Note** that you do not have any change in hand at first.

Given an integer array `bills` where `bills[i]` is the bill the `ith` customer pays, return `true` if you can provide every customer with the correct change, or `false` otherwise.

### Example Cases
1. Case 1:
>Input: `bills = [5,5,5,10,20]`
>
>Output: true
>
>Explanation:
>
>From the first 3 customers, we collect three $5 bills in order.
>
>From the fourth customer, we collect a $10 bill and give back a $5.
>
>From the fifth customer, we give a $10 bill and a $5 bill.
>
>Since all customers got correct change, we output true.

2. Case 2:
>Input: `bills = [5,5,10,10,20]`
>
>Output: false
>
>Explanation: 
>
>From the first two customers in order, we collect two $5 bills.
>
>For the next two customers in order, we collect a $10 bill and give back a $5 bill.
>
>For the last customer, we can not give the change of $15 back because we only have two $10 bills.
>
>Since not every customer received the correct change, the answer is false.

### Constraints
`1 < = bills.length < = 10^5`

`bills[i]` is either `5`, `10`, or `20`.

---
## Python Solution

```python
def lemonadeChange(bills):
    five, ten = 0, 0  # Counters for $5 and $10 bills

    for bill in bills:
        if bill == 5:
            five += 1
        elif bill == 10:
            if five > 0:
                five -= 1
                ten += 1
            else:
                return False
        elif bill == 20:
            if ten > 0 and five > 0:
                ten -= 1
                five -= 1
            elif five >= 3:
                five -= 3
            else:
                return False
    return True
```

---

## Explanation of the Solution

1. **Initialization**:
   - Maintain two counters, `five` and `ten`, to keep track of $5 and $10 bills collected.

2. **Processing Each Bill**:
   - If a customer pays with a $5 bill:
     - Increase the count of `$5` bills.
   - If a customer pays with a $10 bill:
     - Check if you have at least one `$5` bill to give as change. If yes, decrement `five` and increment `ten`.
     - If no `$5` bill is available, return `False`.
   - If a customer pays with a $20 bill:
     - Prioritize giving change using one `$10` and one `$5` bill (if available).
     - If not, attempt to use three `$5` bills.
     - If neither condition is met, return `False`.

3. **Final Result**:
   - If all transactions are processed successfully, return `True`.

## Example Walkthrough

**Input:**
```python
bills = [5, 5, 10, 20, 20]
```
1. **Customer 1** pays with `$5`:
   - `five = 1, ten = 0`

2. **Customer 2** pays with `$5`:
   - `five = 2, ten = 0`

3. **Customer 3** pays with `$10`:
   - Use one `$5` bill for change.
   - `five = 1, ten = 1`

4. **Customer 4** pays with `$20`:
   - Use one `$10` and one `$5` for change.
   - `five = 0, ten = 0`

5. **Customer 5** pays with `$20`:
   - Cannot provide change (no `$5` bills left).
   - Return `False`.

**Output:** `False`
