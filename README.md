```graphql
# schema-codegen-start
const typeDefs = `
  type CreditUnion {
    id: ID!
    Contract_Number: String!
    Credit_Union_Name: String!
    Premium_Reports: [PremiumReport]
    Premium_Adjustments: [PremiumAdjustment]
    Single_Premium_Certificate_Returns: [SinglePremiumCertificateReturn]
  }

  type PremiumReport {
    id: ID!
    Premium_Reports: [PremiumReport]
  }

  type PremiumAdjustment {
    id: ID!
    Product_Name: String!
    Report_Period: String!
    Status: String!
    Last_Update: String!
    Period_Ending: String!
    Adjustment_Type_to_the_Credit_Union: String!
    Comment: String!
    Total_Borrower_Fees_: Float!
    CU_Retail_Rate: Float!
    Protected_Loan_Amount: Float!
    Pay_Rate: Float!
    Premium_Due: Float!
    Total_Amount: Float!
  }

  type SinglePremiumCertificateReturn {
    id: ID!
    Single_Premium_Certificate_Returns: [SinglePremiumCertificateReturn]
  }

  input CreditUnionInput {
    id: ID
    Contract_Number: String!
    Credit_Union_Name: String!
  }

  type Query {
    getCreditUnions: [CreditUnion]
  }

  type Mutation {
    searchCreditUnions(input: CreditUnionInput): [CreditUnion]
  }
`;
# schema-codegen-end
```

```javascript
// resolver-codegen-start
const resolvers = {
  Query: {
    getCreditUnions: () => {
      return [
        {
          id: "1",
          Contract_Number: "123456",
          Credit_Union_Name: "ABC Credit Union",
          Premium_Reports: [],
          Premium_Adjustments: [],
          Single_Premium_Certificate_Returns: []
        },
        {
          id: "2",
          Contract_Number: "789012",
          Credit_Union_Name: "XYZ Credit Union",
          Premium_Reports: [],
          Premium_Adjustments: [],
          Single_Premium_Certificate_Returns: []
        }
      ];
    },
  },
  Mutation: {
    searchCreditUnions: (_, { input }) => {
      const sampleData = [
        {
          id: "1",
          Contract_Number: "123456",
          Credit_Union_Name: "ABC Credit Union",
          Premium_Adjustments: [
            {
              id: "3",
              Product_Name: "Product A",
              Report_Period: "Q1 2023",
              Status: "Active",
              Last_Update: "2023-04-01",
              Period_Ending: "2023-03-31",
              Adjustment_Type_to_the_Credit_Union: "Increase",
              Comment: "Monthly",
              Total_Borrower_Fees_: 100.00,
              CU_Retail_Rate: 2.5,
              Protected_Loan_Amount: 1050.00,
              Pay_Rate: 3.0,
              Premium_Due: 30.00,
              Total_Amount: 1080.00
            }
          ],
        }
      ];
      return sampleData.filter(creditUnion => 
        (!input.id || creditUnion.id === input.id) &&
        (!input.Contract_Number || creditUnion.Contract_Number === input.Contract_Number) &&
        (!input.Credit_Union_Name || creditUnion.Credit_Union_Name === input.Credit_Union_Name)
      );
    }
  }
};
# resolver-codegen-end
```