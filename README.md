# tf-pay
Add a pay with Tf button to any site.
Just include the following 2 lines
``` html
<script src="./tf-pay.min.js"></script>
<tf-pay receiver="walletaddress" amount="1" message="Happy birthday"></tf-pay>
```
| Prop | Description | Required |
| ---- | ------------| -------- |
| receiver | Address to where the tokens should be sent | Yes |
| amount | Amount of tokens to send | Yes |
| message | The message to be included with the transaction, also known as a memo | No (default: empty) |
| asset | The asset type used for the transaction | No (default: tft) |

# For Devs
## Project setup
```
yarn
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
Create a new tf-pay.js file
```
yarn build:wc
```
