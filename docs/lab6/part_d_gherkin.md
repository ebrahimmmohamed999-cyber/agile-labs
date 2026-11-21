# Part D – Gherkin scenarios for our team story

> ⚠️ EXAMPLE ONLY – replace the story and scenarios with ONE story from YOUR team backlog.

**Story:** As a student, I want to pay my tuition invoice online so that I do not queue at the cashier.

```gherkin
Feature: Pay tuition online

  Scenario: Pay the full invoice (happy path)
    Given a student with an unpaid invoice of 7200 EGP
    When the student pays 7200 EGP by card
    Then the invoice is marked as "paid"
    And the student receives a payment receipt

  Scenario: Payment refused because the card is declined (error case)
    Given a student with an unpaid invoice of 7200 EGP
    When the student pays with a declined card
    Then the payment is refused with "card declined"
    And the invoice stays "unpaid"

  Scenario Outline: Partial payments (edge case)
    Given a student with an unpaid invoice of 7200 EGP
    When the student pays <amount> EGP
    Then the invoice status is "<status>"

    Examples:
      | amount | status         |
      | 7200   | paid           |
      | 3600   | partially paid |
      | 0      | unpaid         |
```
