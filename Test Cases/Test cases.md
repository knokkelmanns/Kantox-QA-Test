
**Requirements review**
Before we start creating test cases, we need to analyze the requirements. And there is exist some questions.
- First rule. Should it apply to one type of product or not? If not, which product should be free? How should we decide 
which product should be free (cheaper or with higher cost)? If it relates to one type of product, we need to document that.
- Second rule. Should it apply to one type of product or not? Document this after elaboration.
- Third rule. Does it apply for one type of product or to the total Cart amount? Document this after elaboration.


# Test Cases

| Test Id | Description                                                                                                             | Test Data                                       | Test Steps                                                                | Expected result                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|---------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| TC01    | Checking for an empty Cart                                                                                              | priv/assets/products.yml, priv/assets/rules.yml | Open the cart                                                             | No rule has been applied                                                                                              |
| TC02    | The "buy one, get one free" rule does not apply when adding 1 product                                                   | priv/assets/products.yml                        | Add 1 Green Tea (GR1) to the cart                                         | No rule has been applied. The total price is £3.11                                                                    |
| TC03    | The "buy one, get one free" rule does not apply when adding 2 different products                                        | priv/assets/products.yml, priv/assets/rules.yml | Add 1 Green Tea (GR1) and 1 Strawberries (SR1) to the cart                | No rule has been applied. The total price is £8.11                                                                    |
| TC04    | The "buy one, get one free" rule applies when adding 2 identical products                                               | priv/assets/products.yml, priv/assets/rules.yml | Add 2 Green Tea (GR1) to the cart                                         | The rule has been applied. The total price is £3.11                                                                   |
| TC05    | The "buy one, get one free" rule only applies to an even number of identical products                                   | priv/assets/products.yml, priv/assets/rules.yml | Add 3 Green Tea (GR1) to the cart                                         | The rule has been applied. The total price is £6.22                                                                   |
| TC06    | The "buy > N products, pay X price per product" rule does not apply when N or fewer products are added to the Cart      | priv/assets/products.yml, priv/assets/rules.yml | Add N Strawberries (SR1) to the cart                                      | No rule has been applied. The total price is N * £5.00                                                                |
| TC07    | The "buy > N products, pay X price per product" rule applies when more than N products are added to the Cart            | priv/assets/products.yml, priv/assets/rules.yml | Add N+1 Strawberries (SR1) to the cart                                    | The rule has been applied. The total price is (N+1) * X                                                               |
| TC08    | The "buy > N products, pay X% of the original price" rule does not apply when N or fewer products are added to the Cart | priv/assets/products.yml, priv/assets/rules.yml | Add N Coffee (CF1) to the cart                                            | No rule has been applied. The total price is N * £11.23                                                               |
| TC09    | The "buy > N products, pay X% of the original price" rule applies when more than N products are added to the Cart       | priv/assets/products.yml, priv/assets/rules.yml | Add N+1 Coffee (CF1) to the cart                                          | The rule has been applied. The total price is (N+1) * £11.23 * X%                                                     |
| TC10    | Combination of Special rules                                                                                            | priv/assets/products.yml, priv/assets/rules.yml | Add 2 Green Tea (GR1), N+1 Strawberries (SR1), 1 Coffee (CF1) to the cart | The rules has been applied. The total price is £3.11 (GR1 + 1 free) + SR1 ((N+1) * £5.00 * X%) + normal price for CF1 |
| TC11    | Special rules file (YAML) not connected (missing)                                                                       | priv/assets/products.yml                        | Add 2 Coffee (CF1) to the cart                                            | No rule has been applied. The total price is £22.46                                                                   |
