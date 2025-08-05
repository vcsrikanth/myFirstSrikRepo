# Component Documentation

This directory contains documentation for all reusable components in the project.

## Documentation Template

When documenting components, use the following template:

### Component Template

```markdown
# ComponentName

Brief description of what this component does and when to use it.

## Import

```javascript
// ES6 Import
import { ComponentName } from './components/ComponentName';

// CommonJS
const { ComponentName } = require('./components/ComponentName');
```

## Props/Attributes

### Required Props
- `prop1` (string) - Description of required prop
- `prop2` (number) - Description of another required prop

### Optional Props
- `prop3` (boolean, default: false) - Description of optional prop
- `prop4` (array, default: []) - Description of array prop
- `prop5` (object, default: {}) - Description of object prop
- `className` (string) - Additional CSS classes to apply
- `style` (object) - Inline styles to apply

## Events

- `onEvent1` (function) - Called when event occurs
  - **Parameters**: `(eventData: object) => void`
- `onEvent2` (function) - Called when another event occurs
  - **Parameters**: `(value: string, index: number) => void`

## Usage Examples

### Basic Usage
```jsx
<ComponentName 
  prop1="value1"
  prop2={42}
/>
```

### Advanced Usage
```jsx
<ComponentName 
  prop1="value1"
  prop2={42}
  prop3={true}
  prop4={['item1', 'item2']}
  prop5={{ key: 'value' }}
  className="custom-class"
  style={{ margin: '10px' }}
  onEvent1={(data) => console.log('Event occurred:', data)}
  onEvent2={(value, index) => console.log('Value changed:', value, index)}
/>
```

### With Children
```jsx
<ComponentName prop1="value1">
  <div>Child content</div>
</ComponentName>
```

## Styling

### CSS Classes
- `.component-name` - Root container class
- `.component-name__element` - Element class (BEM methodology)
- `.component-name--modifier` - Modifier class

### CSS Variables
```css
:root {
  --component-primary-color: #007bff;
  --component-secondary-color: #6c757d;
  --component-border-radius: 4px;
  --component-padding: 12px;
}
```

### Custom Styling Example
```css
.my-custom-component {
  --component-primary-color: #28a745;
  border: 2px solid var(--component-primary-color);
}
```

## Accessibility

- **ARIA Roles**: Describes the ARIA roles used
- **Keyboard Navigation**: Describes keyboard shortcuts and navigation
- **Screen Reader Support**: How the component works with screen readers
- **Focus Management**: How focus is handled

### Accessibility Example
```jsx
<ComponentName 
  aria-label="Descriptive label"
  role="button"
  tabIndex={0}
  onKeyDown={(e) => {
    if (e.key === 'Enter' || e.key === ' ') {
      // Handle activation
    }
  }}
/>
```

## Dependencies

- **External Libraries**: List any external dependencies
- **Internal Components**: List any internal component dependencies
- **Utilities**: List any utility function dependencies

## Browser Support

- **Modern Browsers**: Chrome 70+, Firefox 65+, Safari 12+, Edge 79+
- **Mobile**: iOS Safari 12+, Chrome Mobile 70+
- **Polyfills Required**: List any required polyfills for older browsers

## Performance Considerations

- **Bundle Size**: Approximate impact on bundle size
- **Rendering Performance**: Notes about rendering performance
- **Memory Usage**: Any memory considerations
- **Optimization Tips**: Tips for optimal usage

## Testing

### Unit Tests
```javascript
import { render, fireEvent, screen } from '@testing-library/react';
import { ComponentName } from './ComponentName';

test('renders component with required props', () => {
  render(<ComponentName prop1="test" prop2={123} />);
  expect(screen.getByText('test')).toBeInTheDocument();
});

test('handles events correctly', () => {
  const mockHandler = jest.fn();
  render(
    <ComponentName 
      prop1="test" 
      prop2={123} 
      onEvent1={mockHandler} 
    />
  );
  
  fireEvent.click(screen.getByRole('button'));
  expect(mockHandler).toHaveBeenCalledWith(expect.any(Object));
});
```

## Troubleshooting

### Common Issues

**Issue**: Component doesn't render
- **Cause**: Missing required props
- **Solution**: Ensure all required props are provided

**Issue**: Styling doesn't apply
- **Cause**: CSS not imported or conflicting styles
- **Solution**: Import component CSS and check for style conflicts

**Issue**: Events not firing
- **Cause**: Event handlers not properly bound
- **Solution**: Ensure event handlers are functions and properly bound

## Migration Guide

If this component replaces an older version, provide migration instructions:

### From v1.x to v2.x
- `oldProp` has been renamed to `newProp`
- `deprecatedEvent` has been removed, use `newEvent` instead
- CSS class `old-class` is now `new-class`

## Related Components

- **SimilarComponent**: Brief description and link
- **ParentComponent**: Brief description and link
- **ChildComponent**: Brief description and link
```

## Framework-Specific Examples

### React Component Example

```jsx
import React, { useState, useEffect } from 'react';
import PropTypes from 'prop-types';

/**
 * Button component with multiple variants and states
 * 
 * @param {Object} props - Component props
 * @param {string} props.variant - Button variant: 'primary', 'secondary', 'danger'
 * @param {string} props.size - Button size: 'small', 'medium', 'large'
 * @param {boolean} props.disabled - Whether button is disabled
 * @param {boolean} props.loading - Whether button is in loading state
 * @param {function} props.onClick - Click handler
 * @param {React.ReactNode} props.children - Button content
 */
const Button = ({ 
  variant = 'primary', 
  size = 'medium', 
  disabled = false, 
  loading = false, 
  onClick, 
  children,
  ...props 
}) => {
  const [isPressed, setIsPressed] = useState(false);

  const handleClick = (event) => {
    if (disabled || loading) return;
    onClick?.(event);
  };

  const handleKeyDown = (event) => {
    if (event.key === 'Enter' || event.key === ' ') {
      event.preventDefault();
      setIsPressed(true);
      handleClick(event);
    }
  };

  const handleKeyUp = (event) => {
    if (event.key === 'Enter' || event.key === ' ') {
      setIsPressed(false);
    }
  };

  const className = [
    'btn',
    `btn--${variant}`,
    `btn--${size}`,
    disabled && 'btn--disabled',
    loading && 'btn--loading',
    isPressed && 'btn--pressed'
  ].filter(Boolean).join(' ');

  return (
    <button
      className={className}
      disabled={disabled || loading}
      onClick={handleClick}
      onKeyDown={handleKeyDown}
      onKeyUp={handleKeyUp}
      aria-pressed={isPressed}
      aria-busy={loading}
      {...props}
    >
      {loading && <span className="btn__spinner" aria-hidden="true" />}
      <span className="btn__content">{children}</span>
    </button>
  );
};

Button.propTypes = {
  variant: PropTypes.oneOf(['primary', 'secondary', 'danger']),
  size: PropTypes.oneOf(['small', 'medium', 'large']),
  disabled: PropTypes.bool,
  loading: PropTypes.bool,
  onClick: PropTypes.func,
  children: PropTypes.node.isRequired,
};

export default Button;
```

### Vue Component Example

```vue
<template>
  <button
    :class="buttonClasses"
    :disabled="disabled || loading"
    :aria-pressed="isPressed"
    :aria-busy="loading"
    @click="handleClick"
    @keydown="handleKeyDown"
    @keyup="handleKeyUp"
  >
    <span v-if="loading" class="btn__spinner" aria-hidden="true"></span>
    <span class="btn__content">
      <slot></slot>
    </span>
  </button>
</template>

<script>
/**
 * Button component with multiple variants and states
 */
export default {
  name: 'Button',
  props: {
    /**
     * Button variant
     * @type {String}
     * @default 'primary'
     */
    variant: {
      type: String,
      default: 'primary',
      validator: (value) => ['primary', 'secondary', 'danger'].includes(value)
    },
    /**
     * Button size
     * @type {String}
     * @default 'medium'
     */
    size: {
      type: String,
      default: 'medium',
      validator: (value) => ['small', 'medium', 'large'].includes(value)
    },
    /**
     * Whether button is disabled
     * @type {Boolean}
     * @default false
     */
    disabled: {
      type: Boolean,
      default: false
    },
    /**
     * Whether button is in loading state
     * @type {Boolean}
     * @default false
     */
    loading: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      isPressed: false
    };
  },
  computed: {
    buttonClasses() {
      return [
        'btn',
        `btn--${this.variant}`,
        `btn--${this.size}`,
        {
          'btn--disabled': this.disabled,
          'btn--loading': this.loading,
          'btn--pressed': this.isPressed
        }
      ];
    }
  },
  methods: {
    handleClick(event) {
      if (this.disabled || this.loading) return;
      /**
       * Emitted when button is clicked
       * @event click
       * @param {Event} event - Click event
       */
      this.$emit('click', event);
    },
    handleKeyDown(event) {
      if (event.key === 'Enter' || event.key === ' ') {
        event.preventDefault();
        this.isPressed = true;
        this.handleClick(event);
      }
    },
    handleKeyUp(event) {
      if (event.key === 'Enter' || event.key === ' ') {
        this.isPressed = false;
      }
    }
  }
};
</script>
```

### Angular Component Example

```typescript
import { Component, Input, Output, EventEmitter } from '@angular/core';

/**
 * Button component with multiple variants and states
 * 
 * @example
 * <app-button 
 *   variant="primary" 
 *   size="medium"
 *   [disabled]="false"
 *   [loading]="false"
 *   (click)="handleClick($event)">
 *   Click me
 * </app-button>
 */
@Component({
  selector: 'app-button',
  template: `
    <button
      [class]="buttonClasses"
      [disabled]="disabled || loading"
      [attr.aria-pressed]="isPressed"
      [attr.aria-busy]="loading"
      (click)="handleClick($event)"
      (keydown)="handleKeyDown($event)"
      (keyup)="handleKeyUp($event)">
      <span *ngIf="loading" class="btn__spinner" aria-hidden="true"></span>
      <span class="btn__content">
        <ng-content></ng-content>
      </span>
    </button>
  `,
  styleUrls: ['./button.component.css']
})
export class ButtonComponent {
  /**
   * Button variant
   */
  @Input() variant: 'primary' | 'secondary' | 'danger' = 'primary';
  
  /**
   * Button size
   */
  @Input() size: 'small' | 'medium' | 'large' = 'medium';
  
  /**
   * Whether button is disabled
   */
  @Input() disabled: boolean = false;
  
  /**
   * Whether button is in loading state
   */
  @Input() loading: boolean = false;
  
  /**
   * Emitted when button is clicked
   */
  @Output() click = new EventEmitter<Event>();
  
  isPressed: boolean = false;
  
  get buttonClasses(): string {
    return [
      'btn',
      `btn--${this.variant}`,
      `btn--${this.size}`,
      this.disabled ? 'btn--disabled' : '',
      this.loading ? 'btn--loading' : '',
      this.isPressed ? 'btn--pressed' : ''
    ].filter(Boolean).join(' ');
  }
  
  handleClick(event: Event): void {
    if (this.disabled || this.loading) return;
    this.click.emit(event);
  }
  
  handleKeyDown(event: KeyboardEvent): void {
    if (event.key === 'Enter' || event.key === ' ') {
      event.preventDefault();
      this.isPressed = true;
      this.handleClick(event);
    }
  }
  
  handleKeyUp(event: KeyboardEvent): void {
    if (event.key === 'Enter' || event.key === ' ') {
      this.isPressed = false;
    }
  }
}
```

## Component Documentation Checklist

When documenting a new component, ensure you include:

- [ ] Component name and purpose
- [ ] Import/usage instructions
- [ ] All props/attributes with types and descriptions
- [ ] All events with parameters
- [ ] Basic and advanced usage examples
- [ ] Styling information (CSS classes, variables)
- [ ] Accessibility considerations
- [ ] Dependencies and requirements
- [ ] Browser support information
- [ ] Performance considerations
- [ ] Unit test examples
- [ ] Common troubleshooting issues
- [ ] Migration guide (if applicable)
- [ ] Related components

## Storybook Integration

If using Storybook for component documentation:

```javascript
// Button.stories.js
export default {
  title: 'Components/Button',
  component: Button,
  argTypes: {
    variant: {
      control: { type: 'select' },
      options: ['primary', 'secondary', 'danger'],
    },
    size: {
      control: { type: 'select' },
      options: ['small', 'medium', 'large'],
    },
    disabled: { control: 'boolean' },
    loading: { control: 'boolean' },
  },
};

const Template = (args) => <Button {...args}>Button Text</Button>;

export const Primary = Template.bind({});
Primary.args = {
  variant: 'primary',
};

export const Secondary = Template.bind({});
Secondary.args = {
  variant: 'secondary',
};

export const Loading = Template.bind({});
Loading.args = {
  loading: true,
};
```