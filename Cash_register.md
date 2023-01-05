### Cash Register

Design a cash register drawer function checkCashRegister() that accepts purchase price as the first argument (price), payment as the second argument (cash), and cash-in-drawer (cid) as the third argument.

cid is a 2D array listing available currency.

The checkCashRegister() function should always return an object with a status key and a change key.

Return {status: "INSUFFICIENT_FUNDS", change: []} if cash-in-drawer is less than the change due, or if you cannot return the exact change.

Return {status: "CLOSED", change: [...]} with cash-in-drawer as the value for the key change if it is equal to the change due.

Otherwise, return {status: "OPEN", change: [...]}, with the change due in coins and bills, sorted in highest to lowest order, as the value of the change key.
Currency Unit	Amount
Penny	$0.01 (PENNY)
Nickel	$0.05 (NICKEL)
Dime	$0.1 (DIME)
Quarter	$0.25 (QUARTER)
Dollar	$1 (ONE)
Five Dollars	$5 (FIVE)
Ten Dollars	$10 (TEN)
Twenty Dollars	$20 (TWENTY)
One-hundred Dollars	$100 (ONE HUNDRED)

See below for an example of a cash-in-drawer array:

[
  ["PENNY", 1.01],
  ["NICKEL", 2.05],
  ["DIME", 3.1],
  ["QUARTER", 4.25],
  ["ONE", 90],
  ["FIVE", 55],
  ["TEN", 20],
  ["TWENTY", 60],
  ["ONE HUNDRED", 100]
]


## Code 

```javascript
function checkCashRegister(price, cash, cid) {
  const INSUFFICIENT_FUNDS = { status: 'INSUFFICIENT_FUNDS', change: [] };
  const CLOSED = { status: 'CLOSED', change: cid };
  const OPEN = { status: 'OPEN', change: [] };
  let totalCid = cidTotal();
  let dueBlance = parseFloat((cash - price).toFixed(2));

  if (totalCid < dueBlance) {
    return INSUFFICIENT_FUNDS;
  }

  if (totalCid === dueBlance) {
    return CLOSED;
  }

  let cashTypes = [
    ['ONE HUNDRED', 100],
    ['TWENTY', 20],
    ['TEN', 10],
    ['FIVE', 5],
    ['ONE', 1],
    ['QUARTER', 0.25],
    ['DIME', 0.1],
    ['NICKEL', 0.05],
    ['PENNY', 0.01],
  ];

  for (let i = 0; i < cashTypes.length; i++) {
    let cashType = cashTypes[i][0];
    let cashValue = cashTypes[i][1];
    let totalCash = cid.find(item => item[0] === cashType)[1];

    if (dueBlance > cashValue && dueBlance > totalCash) {
      dueBlance -= totalCash;
      OPEN.change.push([cashType, totalCash]);
    } else if (dueBlance > cashValue && totalCash > dueBlance) {
      let pay = Math.floor(dueBlance / cashValue) * cashValue;
      dueBlance -= pay;
      dueBlance = parseFloat(dueBlance.toFixed(2));
      OPEN.change.push([cashType, pay]);
    }
  }

  if (dueBlance > 0) {
    return INSUFFICIENT_FUNDS;
  }

  return OPEN;

  function cidTotal() {
    return parseFloat(cid.reduce((a, b) => a + b[1], 0).toFixed(2));
  }
}

checkCashRegister(19.5, 20, [["PENNY", 1.01], ["NICKEL", 2.05], ["DIME", 3.1], ["QUARTER", 4.25], ["ONE", 90], ["FIVE", 55], ["TEN", 20], ["TWENTY", 60], ["ONE HUNDRED", 100]]);
```
