---

title: 'Business Rule Task'
category: 'Tasks'

keywords: 'service task business rule'

---

A Business Rule task is used to synchronously execute one or more rules.

<div data-bpmn-symbol="businessruletask" data-bpmn-symbol-name="Businss Rule Task"></div>

You might use the rule engine of your choice, on the open source side we made good experiences with JBoss Drools. Therefor You have to plug in your implementation of the rule task exactly like in a Service Task. So the difference is only that it has a different icon in the BPMN process model - but this can make already a huge difference for acceptance of the process model.

```xml
<businessRuleTask id="businessRuleTask" camunda:delegateExpression="${MyRuleServiceDelegate}" />
```

## camunda Extensions

<table class="table table-striped">
  <tr>
    <th>Attributes</th>
    <td>
      <a href="ref:#custom-extensions-camunda-extension-attributes-camundaasync">camunda:async</a>,
      <a href="ref:#custom-extensions-camunda-extension-attributes-camundaclass">camunda:class</a>,
      <a href="ref:#custom-extensions-camunda-extension-attributes-camundadelegateexpression">camunda:delegateExpression</a>,
      <a href="ref:#custom-extensions-camunda-extension-attributes-camundaexclusive">camunda:exclusive</a>,
      <a href="ref:#custom-extensions-camunda-extension-attributes-camundaexpression">camunda:expression</a>,
      <a href="ref:#custom-extensions-camunda-extension-attributes-camundaresultvariable">camunda:resultVariable</a>,
      <a href="ref:#custom-extensions-camunda-extension-attributes-camundatype">camunda:type</a>
    </td>
  </tr>
  <tr>
    <th>Extension Elements</th>
    <td>
      <a href="ref:#custom-extensions-camunda-extension-elements-camundafailedjobretrytimecycle">camunda:failedJobRetryTimeCycle</a>,
      <a href="ref:#custom-extensions-camunda-extension-elements-camundafield">camunda:field</a>
    </td>
  </tr>
  <tr>
    <th>Constraints</th>
    <td>
      One of the attributes <code>camunda:class</code>, <code>camunda:delegateExpression</code>,
      <code>camunda:type</code> or <code>camunda:expression</code> is mandatory
    </td>
  </tr>
  <tr>
    <td></td>
    <td>
      The attribute <code>camunda:resultVariable</code> can only be used in combination with the
      <code>camunda:expression</code> attribute
    </td>
  </tr>
  <tr>
    <td></td>
    <td>
      The <code>camunda:exclusive</code> attribute is only evaluated if the attribute
      <code>camunda:async</code> is set to <code>true</code>
    </td>
  </tr>
</table>

## Additional Resources

* [Service Task](ref:/api-references/bpmn20/#tasks-service-task)
* [Tasks in the BPMN Tutorial](http://camunda.org/design/reference.html#!/activities/tasks)
* [Demo using Drools on the Business Rule Task](https://github.com/camunda/camunda-consulting/tree/master/showcases/order-confirmation-rules)