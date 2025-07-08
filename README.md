# **Fi MCP Documentation**

## **Overview**

The Fi MCP (Model Context Protocol) provides access to comprehensive financial data for users of the Fi Money platform. This MCP  enables developers to build applications that can analyze users' financial health, provide insights, and create personalized financial recommendations based on real account data.

## **Available Tools**

### **1\. `fetch_net_worth`**

**Purpose**: Calculate comprehensive net worth using actual data from connected accounts

**Use Cases**:

* Portfolio analysis and asset allocation insights  
* Net worth tracking and visualization  
* Financial health assessments  
* Investment performance analysis  
* Debt-to-asset ratio calculations

**Data Sources**:

* Bank account balances  
* Mutual fund holdings and current values  
* Indian stock portfolio holdings  
* US stock investments (if invested through Fi Money app)
* EPF account balances
* Credit card debt and loan balances  
* Other connected assets/liabilities

<details>
  <summary>Response Format</summary>
  
```json
{
  "netWorthResponse": {
    "totalNetWorthValue": {
      "currencyCode": "string" // e.g. INR
      "units": "string" // e.g. total net worth amount
    },
    "assetValues": [
      {
        "netWorthAttribute": "string" // e.g. ASSET_TYPE_EPF
        "value": {
          "currencyCode": "string" // e.g. INR
          "units": "string" // e.g. individual asset value
        }
      }
      // Only one sample asset shown
    ]
  },
  "mfSchemeAnalytics": {
    "schemeAnalytics": [
      {
        "schemeDetail": {
          "amc": "string" // e.g. QUANT_MONEY_MANAGERS
          "nameData": {
            "longName": "string" // e.g. fund name
          },
          "planType": "string" // e.g. DIRECT
          "investmentType": "string" // e.g. OPEN
          "optionType": "string" // e.g. GROWTH
          "nav": {
            "currencyCode": "string" // e.g. INR
            "units": "string" // e.g. NAV whole part
            "nanos": "number" // e.g. NAV fractional part
          },
          "assetClass": "string" // e.g. EQUITY
          "isinNumber": "string" // e.g. INF123L01234
          "categoryName": "string" // e.g. ELSS_TAX_SAVING
          "fundhouseDefinedRiskLevel": "string" // e.g. VERY_HIGH_RISK
        },
        "enrichedAnalytics": {
          "analytics": {
            "schemeDetails": {
              "currentValue": {
                "currencyCode": "string"
                "units": "string"
                "nanos": "number"
              },
              "investedValue": {
                "currencyCode": "string"
                "units": "string"
                "nanos": "number"
              },
              "XIRR": "number" // e.g. % return
              "absoluteReturns": {
                "currencyCode": "string"
                "units": "string"
                "nanos": "number"
              },
              "unrealisedReturns": {
                "currencyCode": "string"
                "units": "string"
                "nanos": "number"
              },
              "navValue": {
                "currencyCode": "string"
                "units": "string"
                "nanos": "number"
              },
              "units": "number" // e.g. 123.01
            }
          }
        }
      }
    ]
  },
  "accountDetailsBulkResponse": {
    "accountDetailsMap": {
      "accountId": {
        "accountDetails": {
          "fipId": "string" // e.g. KotakMahindraBank-FIP
          "maskedAccountNumber": "string" // e.g. XXXXXX1234
          "accInstrumentType": "string" // e.g. ACC_INSTRUMENT_TYPE_DEPOSIT
          "ifscCode": "string" // e.g. ABCD0000123
          "accountType": {
            "depositAccountType": "string" // e.g. DEPOSIT_ACCOUNT_TYPE_SAVINGS
          },
          "fipMeta": {
            "name": "string" // e.g. Kotak Mahindra Bank
            "displayName": "string" // e.g. Kotak
            "bank": "string" // e.g. KOTAK
          }
        },
        "depositSummary": {
          "accountId": "string"
          "currentBalance": {
            "currencyCode": "string"
            "units": "string"
            "nanos": "number"
          },
          "balanceDate": "ISODate" // e.g. 2025-01-01T11:59:59.149Z
          "depositAccountType": "string"
          "branch": "string"
          "ifscCode": "string"
          "openingDate": "ISODate"
          "depositAccountStatus": "string"
        },
        "equitySummary": {
          "accountId": "string"
          "currentValue": {
            "currencyCode": "string"
            "units": "string"
            "nanos": "number"
          },
          "holdingsInfo": [
            {
              "isin": "string" // e.g. INE00H001014
              "issuerName": "string" // e.g. EPIFI LIMITED
              "type": "string" // e.g. EQUITY_HOLDING_TYPE_DEMAT
              "units": "number" // e.g. quantity held
              "lastTradedPrice": {
                "currencyCode": "string"
                "units": "string"
                "nanos": "number"
              },
              "isinDescription": "string" // e.g. EPIFI LIMITED-EQ
            }
          ]
        }
      }
    }
  }
}

```

</details>

[Sample response](./sample_responses/fetch_net_worth.json)

**Error Handling**:

* Returns empty result if no financial accounts are connected  
* Prompts users to connect mutual fund accounts if not detected  
* Only includes data from connected accounts (no estimations)

---

### **2\. `fetch_credit_report`**

**Purpose**: Retrieve comprehensive credit report information

**Use Cases**:

* Credit score monitoring  
* Loan prioritization based on interest rates  
* Credit utilization analysis

**Data Included**:

* Credit scores  
* Active, closed loan details with interest rates  
* Credit card utilization rates  
* Recent credit inquiries  
* Date of birth information

<details>
  <summary>Response Format</summary>

```json
{
  "creditReports": [
    {
      "creditReportData": {
        "userMessage": {
          "userMessageText": "string" // e.g. Normal Response
        },
        "creditProfileHeader": {
          "reportDate": "string" // e.g. 20250101
          "reportTime": "string" // e.g. 235959
        },
        "currentApplication": {
          "currentApplicationDetails": {
            "enquiryReason": "string" // e.g. 6
            "amountFinanced": "string" // e.g. 0
            "durationOfAgreement": "string" // e.g. 0
            "currentApplicantDetails": {
              "dateOfBirthApplicant": "string" // e.g. 19690131
            }
          }
        },
        "creditAccount": {
          "creditAccountSummary": {
            "account": {
              "creditAccountTotal": "string" // e.g. 2
              "creditAccountActive": "string" // e.g. 2
              "creditAccountDefault": "string" // e.g. 0
              "creditAccountClosed": "string" // e.g. 0
              "cadSuitFiledCurrentBalance": "string" // e.g. 0
            },
            "totalOutstandingBalance": {
              "outstandingBalanceSecured": "string" // e.g. 10000
              "outstandingBalanceSecuredPercentage": "string" // e.g. 20
              "outstandingBalanceUnSecured": "string" // e.g. 40000
              "outstandingBalanceUnSecuredPercentage": "string" // e.g. 80
              "outstandingBalanceAll": "string" // e.g. 50000
            }
          },
          "creditAccountDetails": [
            {
              "identificationNumber": "string" // e.g. AV12345678
              "subscriberName": "string" // e.g. Federal Bank
              "portfolioType": "string" // e.g. R
              "accountType": "string" // e.g. 10
              "openDate": "string" // e.g. 20250101
              "creditLimitAmount": "string" // e.g. 500000
              "highestCreditOrOriginalLoanAmount": "string" // e.g. 80000
              "accountStatus": "string" // e.g. 11
              "paymentRating": "string" // e.g. 0
              "paymentHistoryProfile": "string" // e.g. 000000000000000000000000?00000000000
              "currentBalance": "string" // e.g. 0
              "amountPastDue": "string" // e.g. 0
              "dateReported": "string" // e.g. 20250701
              "dateOfLastPayment": "string" // e.g. 20250701
              "repaymentTenure": "string" // e.g. 0
              "dateOfAddition": "string" // e.g. 20220101
              "currencyCode": "string" // e.g. INR
              "accountHolderTypeCode": "string" // e.g. 1
            }
          ]
        },
        "matchResult": {
          "exactMatch": "string" // e.g. Y
        },
        "totalCapsSummary": {
          "totalCapsLast7Days": "string" // e.g. 0
          "totalCapsLast30Days": "string" // e.g. 0
          "totalCapsLast90Days": "string" // e.g. 0
          "totalCapsLast180Days": "string" // e.g. 0
        },
        "nonCreditCaps": {
          "nonCreditCapsSummary": {
            "nonCreditCapsLast7Days": "string" // e.g. 0
            "nonCreditCapsLast30Days": "string" // e.g. 0
            "nonCreditCapsLast90Days": "string" // e.g. 0
            "nonCreditCapsLast180Days": "string" // e.g. 0
          }
        },
        "score": {
          "bureauScore": "string" // e.g. 800
        },
        "caps": {
          "capsSummary": {
            "capsLast7Days": "string" // e.g. 0
            "capsLast30Days": "string" // e.g. 0
            "capsLast90Days": "string" // e.g. 0
            "capsLast180Days": "string" // e.g. 0
          },
        }
      },
      "vendor": "EXPERIAN"
    }
  ]
}


```

</details>

[Sample response](./sample_responses/fetch_credit_report.json)

**Error Handling**:

* Returns "No credit score data available" if not connected  
* Prompts users to connect credit profile in Fi Money app

---

### **3\. `fetch_epf_details`**

**Purpose**: Access Employee Provident Fund account information

**Use Cases**:

* Retirement planning calculations  
* EPF contribution tracking  
* Interest earned analysis  
* Employer contribution verification

**Data Included**:

* Current account balance  
* Employer and employment details  
* Total Employee contribution  
* Total Employer contribution

<details>
  <summary>Response Format</summary>

```json
{
  "uanAccounts": [
    {
      "phoneNumber": {}, // object (structure not specified)
      "rawDetails": {
        "est_details": [
          {
            "est_name": "string", // e.g. Company Name
            "member_id": "string", // e.g. RJRAJ12345690000012345
            "office": "string", // e.g. (RO)JAIPUR
            "doj_epf": "string", // e.g. 01-01-2020
            "doe_epf": "string", // e.g. 01-01-2025
            "doe_eps": "string", // e.g. 01-01-2025
            "pf_balance": {
              "is_pf_full_withdrawn": true, // boolean
              "employee_share": {
                "debit": "string", // e.g. 12345
                "credit": "string" // e.g. 12345
              },
              "employer_share": {
                "debit": "string", // e.g. 1234
                "credit": "string" // e.g. 1234
              }
            }
          },
         "overall_pf_balance": {
          "pension_balance": "string", // e.g. 12345
          "current_pf_balance": "string", // e.g. 54321
          "employee_share_total": {
            "debit": "string", // e.g. 12345
            "credit": "string", // e.g. 54321
            "balance": "string" // e.g. 12345
          },
          "employer_share_total": {
            "debit": "string", // e.g. 1234
            "credit": "string", // e.g. 12345
            "balance": "string" // e.g. 123456
          }
        }
      }
    }
  ]
}


```

</details>

[Sample response](./sample_responses/fetch_epf_details.json)

**Error Handling**:

* Directs users to link EPF account through Fi Money app if not connected

---

### 

### **4\. `fetch_mf_transactions`**

**Purpose**: Retrieve mutual funds transaction history for portfolio analysis

**Use Cases**:

* XIRR (Extended Internal Rate of Return) calculations  
* Investment performance tracking  
* Transaction pattern analysis  
* Portfolio rebalancing insights

**Current Scope**:

* Mutual fund transactions (buy, sell, SIP, etc.)  
* Transaction dates and amounts  
* Fund-wise transaction history

<details>
  <summary>Response Format</summary>

```json
{
  "transactions": [
    {
      "isinNumber": "string", // e.g. INF123L01234
      "folioId": "string", // e.g. 1234567890
      "externalOrderType": "string", // e.g. BUY
      "transactionDate": "string", // e.g. 2025-01-01T23:59:59Z (ISO format)
      "purchasePrice": {
        "currencyCode": "string", // e.g. INR
        "units": "string", // e.g. 250
        "nanos": "number" // e.g. 785200000
      },
      "transactionAmount": {
        "currencyCode": "string", // e.g. INR
        "units": "string", // e.g. 9999
        "nanos": "number" // e.g. 500000000
      },
      "transactionUnits": "number", // e.g. 98.765
      "transactionMode": "string", // e.g. N
      "schemeName": "string", // e.g. Epifi Tax Saver Fund - Direct Plan
      "stampDuty": "number" // e.g. 0.1
    }
  ]
}

```

</details>

[Sample response](./sample_responses/fetch_mf_transactions.json)

**Notes on Response Structure**:

* `purchasePrice`: NAV at which transaction was executed  
* `transactionAmount`: Total amount invested/redeemed  
* `transactionUnits`: Number of units bought/sold  
* `transactionMode`: "N" for Normal, other modes may include SIP, etc.  
* `externalOrderType`: "BUY" for purchases, "SELL" for redemptions  
* Amounts use `units` (main amount) and `nanos` (fractional part) structure  
* XIRR calculation needs to be done separately using this transaction data

**Current Limitations**:

* Does NOT include bank transactions  
* Does NOT include stock transaction history  
* No NPS or deposit transaction data  
* Limited to mutual fund transactions only

**Error Handling**:

* Returns available data with clear indication of limitations  
* Specifies which transaction types are not included  
* SIP performance evaluator

## **Integration Guidelines**

### **Error Handling Best Practices**

1. **Connection Status**: Always check if required accounts are connected before displaying data  
2. **Data Availability**: Handle cases where specific data types may not be available  
3. **User Guidance**: Provide clear instructions on how to connect missing accounts  
4. **Graceful Degradation**: Design UI to work with partial data when some accounts aren't connected

### **Security Considerations**

1. **Data Privacy**: Never store or cache sensitive financial data  
2. **Authentication**: Ensure proper user authentication before accessing MCP  
3. **Data Display**: Use appropriate formatting for financial data display

### **Performance Optimization**

1. **Batch Processing**: Group related MCP calls when possible  
2. **Error Recovery**: Implement retry mechanisms for failed calls

**How to create the MCP Client**

Simplest Python MCP client for connecting to server

```py
from mcp.client.streamable_http import streamablehttp_client
from mcp.client.session import ClientSession
import asyncio
 
async def main():
    try:
        async with streamablehttp_client("https://mcp.fi.money:8080/mcp/stream") as (
            read_stream,
            write_stream,
            _,
        ):
            async with ClientSession(
                read_stream,
                write_stream,
            ) as session:
                await session.initialize()
                tools = await session.list_tools()
                print(tools)
    except Exception as e:
        print(f"error: {e}")

if __name__ == "__main__":
    asyncio.run(main())


```

## **Sample Integration Code**

### **Basic Net Worth Fetch**

Javascript snippet

```javascript
async function getUserNetWorth() {
  try {
    const response = await mcp.call('networth:fetch_net_worth');
    if (response.netWorthResponse && response.netWorthResponse.totalNetWorthValue) {
      const totalValue = response.netWorthResponse.totalNetWorthValue.units;
      const assets = response.netWorthResponse.assetValues;
      displayNetWorth(totalValue, assets);
    } else {
      promptAccountConnection();
    }
  } catch (error) {
    handleError(error);
  }
}
```

### **Credit Score Monitoring**

Javascript snippet

```javascript
async function getCreditInsights() {
  try {
    const response = await mcp.call('networth:fetch_credit_report');
    if (response.creditReports && response.creditReports.length > 0) {
      const creditData = response.creditReports[0].creditReportData;
      const score = creditData.score.bureauScore;
      const dateOfBirth = creditData.currentApplication.currentApplicationDetails.currentApplicantDetails.dateOfBirthApplicant;
      const accounts = creditData.creditAccount.creditAccountDetails;
      
      analyzeCreditScore(score, dateOfBirth, accounts);
    } else {
      promptCreditConnection();
    }
  } catch (error) {
    showCreditError();
  }
}
```

### **EPF Balance Tracking**

Javascript snippet

```javascript
async function getEPFDetails() {
  try {
    const response = await mcp.call('networth:fetch_epf_details');
    if (response.uanAccounts && response.uanAccounts.length > 0) {
      const epfData = response.uanAccounts[0].rawDetails;
      const totalBalance = epfData.overall_pf_balance.current_pf_balance;
      const employeeShare = epfData.overall_pf_balance.employee_share_total.balance;
      const employerShare = epfData.overall_pf_balance.employer_share_total.balance;
      
      displayEPFBreakdown(totalBalance, employeeShare, employerShare);
    } else {
      promptEPFConnection();
    }
  } catch (error) {
    handleEPFError();
  }
}
```

### **Mutual Fund XIRR Calculation**

Javascript snippet

```javascript
async function calculatePortfolioXIRR() {
  try {
    const response = await mcp.call('networth:fetch_mf_transactions');
    if (response.transactions && response.transactions.length > 0) {
      const transactions = response.transactions;
      
      // Group transactions by scheme
      const groupedTransactions = transactions.reduce((acc, tx) => {
        if (!acc[tx.isinNumber]) {
          acc[tx.isinNumber] = [];
        }
        acc[tx.isinNumber].push({
          date: new Date(tx.transactionDate),
          amount: parseFloat(tx.transactionAmount.units) + 
                 (tx.transactionAmount.nanos / 1000000000),
          type: tx.externalOrderType
        });
        return acc;
      }, {});
      
      // Calculate XIRR for each scheme
      calculateXIRRByScheme(groupedTransactions);
    } else {
      showNoTransactionsMessage();
    }
  } catch (error) {
    handleTransactionError();
  }
}
```

## **Key Data Structure Notes**

### **Currency Format**

All monetary values in the API use the following structure:

```json
{
  "currencyCode": "INR",
  "units": "string_value",
  "nanos": "numeric_fractional_value"
}
```

* `units`: Main currency amount as string  
* `nanos`: Fractional part (1 nano \= 1/1,000,000,000 of a unit)  
* To get actual value: `parseFloat(units) + (nanos / 1000000000)`

### **Asset Type Mapping**

* `ASSET_TYPE_EPF`: Employee Provident Fund balance  
* `ASSET_TYPE_INDIAN_SECURITIES`: Indian stock holdings  
* `ASSET_TYPE_SAVINGS_ACCOUNTS`: Bank account balances  
* `ASSET_TYPE_MUTUAL_FUND`: Mutual fund portfolio value  
* `ASSET_TYPE_US_SECURITIES`: US stock investments

### **Credit Account Types**

* Account Type "10": Credit Card accounts  
* Account Status "11": Active accounts  
* Payment Rating "0": Current (no delays)

### **Date Formats**

* EPF dates: "DD-MM-YYYY" format  
* Transaction dates: ISO 8601 format ("YYYY-MM-DDTHH:MM:SSZ")  
* Credit report dates: "YYYYMMDD" format

---

### **Common Issues**

* **Partial Data**: Some tools may return limited data based on the accounts user has currently connected  
* **Authentication Errors**: Ensure proper MCP authentication and permissions

### **Best Practices**

* Provide clear error messages with actionable steps  
* Implement proper loading states for async operations

### **Getting Help**

* Check error messages for specific guidance  
* Test with different account connection scenarios

---

*This documentation covers the current version of the Fi MCP. Features and capabilities may be expanded in future versions.*

