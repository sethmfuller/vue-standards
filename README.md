# Vue Standards
Formal standards for how Vue projects should be constructed

## Single File Components

### Script Section
- Order:
  - name
  - props
  - components
  - data
  - computed
  - methods
  - beforeCreate
  - created
  - beforeMount
  - mounted
  - beforeUpdate
  - updated
  - activated
  - deactivated
  - beforeDestroy
  - destroyed
  - errorCaptured

- Selecting DOM Elements:
  - Give elements the `ref="yourName"` attribute and use this.$refs.yourName to access that attribute.
  - Give elements the `class=""` or `id=""` attribute to style the elements
  - Main idea is to keep the different attributes (class, id, and ref) and their uses seperate
