# Part D – Gherkin scenarios for our team story

**Project:** Pharmacy Stock & Expiry Tracker

**Story:** As a pharmacist, I want to be warned about medicines that are close to
their expiry date, so that I can sell or return them before they are wasted.

```gherkin
Feature: Expiry date warning

  Background:
    Given today's date is "2026-11-21"

  Scenario: Medicine close to expiry is flagged (happy path)
    Given the stock has "Panadol" with 20 boxes expiring on "2026-12-10"
    When the pharmacist opens the expiry report
    Then "Panadol" is listed as "expiring soon"
    And the report shows 20 boxes for "Panadol"

  Scenario: Expired medicine cannot be sold (refused case)
    Given the stock has "Augmentin" with 5 boxes expiring on "2026-11-01"
    When the pharmacist tries to sell 1 box of "Augmentin"
    Then the sale is refused with "medicine is expired"
    And the stock of "Augmentin" is still 5 boxes

  Scenario Outline: Status depends on days left until expiry (edge / outline)
    Given the stock has "Brufen" with 10 boxes expiring on "<expiry>"
    When the pharmacist opens the expiry report
    Then "Brufen" is listed as "<status>"

    Examples:
      | expiry     | status        |
      | 2026-11-20 | expired       |
      | 2026-11-21 | expiring soon |
      | 2026-12-21 | expiring soon |
      | 2027-03-01 | ok            |
```