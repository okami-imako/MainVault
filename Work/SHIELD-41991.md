---
tags:
  - jira-ticket
link: https://jira.inside-box.net/browse/SHIELD-41991
---
1. Если отчет не запущен, то барьер нужно удалить с помощью кнопки
2. Если отчет PENDING, то отчет нужно отменить и барьер нужно удалить с помощью кнопки
3. Если отчет DONE и барьер DRAFT, то барьер нужно удалить с помощью кнопки
4. Если отчет DONE и барьер PENDING, то барьер нельзя задизейблить с помощью кнопки - нужно переводить его через апи в ENABLED, потом выключать и удалять с помощью кнопок
5. Если отчет DONE и барьер ENABLED, то барьер нужно выключить и удалить с помощью кнопки
6. Если отчет DONE и барьер DISABLED, то барьер нужно удалить с помощью кнопки

В данный момент:
```Gherkin
    @SHIELD-23116 @P1 @Finally-SHIELD-22067 @Delay-11-hrs @InformationBarriers @not-pr
    Scenario: (Step 6/6) As an admin, I can delete an information barrier and clean up the environment
        Given I am logged in as "shield_multipart_user1"
        And I delete folders with prefix "IB_Multipart_1" in folder with parentID "0"
        And I am logged in as "shield_multipart_user2"
        And I delete folders with prefix "IB_Multipart_2" in folder with parentID "0"
        And I am logged in as "shield_multipart_user3"
        And I delete folders with prefix "IB_Multipart_3" in folder with parentID "0"
        And I am logged in as "shield_multipart_admin"
        And I navigate to the information barriers page
        And I cancel the pending collaboration report if it exists
        When I click on the delete information barrier button
        And I confirm the delete operation on the confirmation modal
        Then I see a success banner notification text
```

Должно быть так:
```Gherkin
    @SHIELD-23116 @P1 @Finally-SHIELD-22067 @Delay-11-hrs @InformationBarriers @not-pr
    Scenario: (Step 6/6) As an admin, I can delete an information barrier and clean up the environment
        Given I am logged in as "shield_multipart_user1"
        And I delete folders with prefix "IB_Multipart_1" in folder with parentID "0"
        And I am logged in as "shield_multipart_user2"
        And I delete folders with prefix "IB_Multipart_2" in folder with parentID "0"
        And I am logged in as "shield_multipart_user3"
        And I delete folders with prefix "IB_Multipart_3" in folder with parentID "0"
        And I am logged in as "shield_multipart_admin"
        And I navigate to the information barriers page
        And I cancel the pending collaboration report if it exists
		And I enable information barrier if pending
		And I disable information barrier if enabled
        When I click on the delete information barrier button
        And I confirm the delete operation on the confirmation modal
        Then I see a success banner notification text
```

[[ib-multipart-e2e-final-step.excalidraw|Block Scheme]]