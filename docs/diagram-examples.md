# Диаграммы

``` mermaid
requirementDiagram

    requirement test_req {
    id: 1
    text: the test text.
    risk: high
    verifyMethod: test
    }

    functionalRequirement test_req2 {
    id: 1.1
    text: the second test text.
    risk: low
    verifyMethod: inspection
    }

    performanceRequirement test_req3 {
    id: 1.2
    text: the third test text.
    risk: medium
    verifyMethod: demonstration
    }

    interfaceRequirement test_req4 {
    id: 1.2.1
    text: the fourth test text.
    risk: medium
    verifyMethod: analysis
    }

    physicalRequirement test_req5 {
    id: 1.2.2
    text: the fifth test text.
    risk: medium
    verifyMethod: analysis
    }

    designConstraint test_req6 {
    id: 1.2.3
    text: the sixth test text.
    risk: medium
    verifyMethod: analysis
    }

    element test_entity {
    type: simulation
    }

    element test_entity2 {
    type: word doc
    docRef: reqs/test_entity
    }

    element test_entity3 {
    type: "test suite"
    docRef: github.com/all_the_tests
    }


    test_entity - satisfies -> test_req2
    test_req - traces -> test_req2
    test_req - contains -> test_req3
    test_req3 - contains -> test_req4
    test_req4 - derives -> test_req5
    test_req5 - refines -> test_req6
    test_entity3 - verifies -> test_req5
    test_req <- copies - test_entity2
```

## Блок схема

``` mermaid
graph LR
  A[Start] --> B{Error?};
  B -->|Yes| C[Hmm...];
  C --> D[Debug];
  D --> B;
  B ---->|No| E[Yay!];
```
## Диаграмма последовательностей

``` mermaid
sequenceDiagram
  autonumber
  Alice->>John: Hello John, how are you?
  loop Healthcheck
      John->>John: Fight against hypochondria
  end
  Note right of John: Rational thoughts!
  John-->>Alice: Great!
  John->>Bob: How about you?
  Bob-->>John: Jolly good!
```
## Диаграмма состояний

``` mermaid
stateDiagram-v2
  state fork_state <<fork>>
    [*] --> fork_state
    fork_state --> State2
    fork_state --> State3

    state join_state <<join>>
    State2 --> join_state
    State3 --> join_state
    join_state --> State4
    State4 --> [*]
```
## Диаграмма классов

``` mermaid
classDiagram
  Person <|-- Student
  Person <|-- Professor
  Person : +String name
  Person : +String phoneNumber
  Person : +String emailAddress
  Person: +purchaseParkingPass()
  Address "1" <-- "0..1" Person:lives at
  class Student{
    +int studentNumber
    +int averageMark
    +isEligibleToEnrol()
    +getSeminarsTaken()
  }
  class Professor{
    +int salary
  }
  class Address{
    +String street
    +String city
    +String state
    +int postalCode
    +String country
    -validate()
    +outputAsLabel()  
  }
```
## Диаграмма сущностей

``` mermaid
erDiagram
  CUSTOMER ||--o{ ORDER : places
  ORDER ||--|{ LINE-ITEM : contains
  LINE-ITEM {
    string name
    int pricePerUnit
  }
  CUSTOMER }|..|{ DELIVERY-ADDRESS : uses
```
``` mermaid
sequenceDiagram
  Actor Customer as User
  participant LoginPage as Log in page
  participant P1 as Log in details storage
  participant P2 as Security Department

  Customer ->>+ LoginPage: Input: Username
  Customer ->>+ LoginPage: Input: Password
  LoginPage ->> P1: Username and password
  P1 ->> P1: Authenticate
  alt Successful Authentication
    LoginPage ->> LoginPage: Redirect to welcome page
    LoginPage ->> Customer: Log in successful, stand by
  else Failed Authentication
  P1 ->> LoginPage: If rejected
  Customer ->> Customer: I forgot my password...
  LoginPage ->> Customer: Password Hint
  Customer ->> Customer: I still can't remember...
end

LoginPage ->> Customer: Do you wish to reset your password
opt Password Reset Flow
  Customer ->> LoginPage: Yes
  LoginPage ->> P2: New password request
  P2 ->> P2: Validate email address
  P2 ->> Customer: Email sent with a reset link
  Customer ->> P2: Input new password
  P2 ->> P2: Process new password
  P2 ->> P1: Store new password
  P2 ->> P2: Redirect user to log in page
end
```
## Тест единого источника
{!equations.md!}
