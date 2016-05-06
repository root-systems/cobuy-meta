# [Value Flows](https://valueflo.ws)

## init

### Agent Types

- Person
- ConsumerCoop (from Group)
- PurchaseGroup (from Group)
- Supplier

### Agents

- people
  - Sarah Rogers
  - ...
- consumer co-ops
  - Petone Fruit & Vege Co-op
  - Petone Dry Goods Co-op
  - ...
- purchase group
  - "People who want to buy from Central Nuts"
  - ...
- suppliers
  - Ceres Organics
  - Central Nuts
  - ...

### Relationship Types

- hasMember: Group -> Person
- adminOf: Person -> ConsumerCoop
- consumesFrom: ConsumerCoop -> Supplier
- hasChild: parent Group -> child Group
- facilitates: Person -> PurchaseGroup
- interestedIn: Person -> PurchaseGroup

### Relationships

examples:

- Sarah - memberOf -> Petone Fruit & Vege Co-op
- Petone Fruit & Vege Co-op - hasChild -> "People who want to buy from Central Nuts"
- Sarah - adminOf -> Petone Fruit & Vege Co-op
- Petone Dry Goods Co-op - consumesFrom -> Ceres Organics
- Sarah - facilitates -> "People who want to buy from Central Nuts"

## co-op member proposes new order

when member proposes new order:

- create new PurchaseGroup
- create 'facilitates' relationship from proposing member to new PurchaseGroup
- create 'hasChild' relationship from parent ConsumerCoop to new PurchaseGroup

as other members "subscribe" to join order:

- create 'interestedIn' relationship from subscribing member to new PurchaseGroup

## facilitator contacts supplier, receives current price list

when facilitator receives "price list":

- for each item in price list,
  - update Resource Type for given item
  - create Commitment from Supplier to offer Resource Type
    - include price per quantity
    - include minimum, discrete, or continuous quantities

## facilitator opens order to rest of members

when facilitator opens order:

- create ConsumerCoop Intent to buy Resources from Supplier

## members express their Intent to buy goods, including their preference for "tweaking" process

when members express their orders:

- create member Intent to buy Resources from Supplier

## order closes, automagic tweaking, reviewed by facilitator

when order closes and after reviewed by faciliator:

- create ConsumerCoop Commitment to receive Resources from Supplier
- export ConsumerCoop Commitment as invoice to Supplier

## supplier sends Resources and invoice Plan to co-op depot

- import invoice from Supplier as Supplier Commitment

## packers [stock-take](https://en.wikipedia.org/wiki/Stock-taking) received Resources to document Reality

- for each item in stock,
  - create Resource for received item
  - create ConsumerCoop Observation for receiving Resource

## packers pack Resources into desired quantities for members

when a packer packs an order:

- create ConsumerCoop Commitment to send Resources to member

## members pick up their orders

when a member picks up an order:

- create ConsumerCoop Observation of sending Resources to member
