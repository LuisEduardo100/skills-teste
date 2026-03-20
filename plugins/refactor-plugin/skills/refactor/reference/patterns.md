# Refactoring Patterns Reference

## Extract Function

**Before:**
```javascript
function processOrder(order) {
  // validate
  if (!order.items || order.items.length === 0) {
    throw new Error('Order must have items');
  }
  if (!order.customer || !order.customer.email) {
    throw new Error('Order must have customer email');
  }

  // calculate total
  let total = 0;
  for (const item of order.items) {
    total += item.price * item.quantity;
    if (item.discount) {
      total -= item.discount;
    }
  }

  // apply tax
  const tax = total * 0.1;
  total += tax;

  return { total, tax };
}
```

**After:**
```javascript
function processOrder(order) {
  validateOrder(order);
  const subtotal = calculateSubtotal(order.items);
  const tax = subtotal * TAX_RATE;
  return { total: subtotal + tax, tax };
}

function validateOrder(order) {
  if (!order.items?.length) {
    throw new Error('Order must have items');
  }
  if (!order.customer?.email) {
    throw new Error('Order must have customer email');
  }
}

function calculateSubtotal(items) {
  return items.reduce((sum, item) => {
    return sum + item.price * item.quantity - (item.discount ?? 0);
  }, 0);
}

const TAX_RATE = 0.1;
```

## Replace Nested Conditionals with Guard Clauses

**Before:**
```python
def get_payment_amount(employee):
    if employee is not None:
        if employee.is_active:
            if employee.role == "contractor":
                return employee.hourly_rate * employee.hours
            else:
                return employee.salary / 12
        else:
            return 0
    else:
        raise ValueError("Employee cannot be None")
```

**After:**
```python
def get_payment_amount(employee):
    if employee is None:
        raise ValueError("Employee cannot be None")
    if not employee.is_active:
        return 0
    if employee.role == "contractor":
        return employee.hourly_rate * employee.hours
    return employee.salary / 12
```

## Replace Magic Numbers with Named Constants

**Before:**
```typescript
if (password.length < 8) { ... }
if (retries > 3) { ... }
setTimeout(callback, 86400000);
```

**After:**
```typescript
const MIN_PASSWORD_LENGTH = 8;
const MAX_RETRIES = 3;
const ONE_DAY_MS = 24 * 60 * 60 * 1000;

if (password.length < MIN_PASSWORD_LENGTH) { ... }
if (retries > MAX_RETRIES) { ... }
setTimeout(callback, ONE_DAY_MS);
```

## Consolidate Conditional Logic

**Before:**
```javascript
function getShippingCost(country) {
  if (country === 'US') return 5.99;
  if (country === 'CA') return 7.99;
  if (country === 'UK') return 9.99;
  if (country === 'DE') return 9.99;
  if (country === 'FR') return 9.99;
  if (country === 'JP') return 12.99;
  if (country === 'AU') return 12.99;
  return 15.99;
}
```

**After:**
```javascript
const SHIPPING_RATES = {
  US: 5.99,
  CA: 7.99,
  UK: 9.99, DE: 9.99, FR: 9.99,
  JP: 12.99, AU: 12.99,
};
const DEFAULT_SHIPPING = 15.99;

function getShippingCost(country) {
  return SHIPPING_RATES[country] ?? DEFAULT_SHIPPING;
}
```

## When NOT to Refactor

- Code that is about to be deleted or replaced
- Code under active development by someone else
- Performance-critical hot paths (readability trade-offs may be intentional)
- Code without tests (add tests first, then refactor)
- One-off scripts or migration code
