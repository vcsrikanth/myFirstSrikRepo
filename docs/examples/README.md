# Examples and Usage Instructions

This directory contains practical examples, tutorials, and usage instructions for the project.

## Quick Start Examples

### Basic HTML Page Setup

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Project</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>Welcome to My Project</h1>
        <nav>
            <ul>
                <li><a href="#home">Home</a></li>
                <li><a href="#about">About</a></li>
                <li><a href="#contact">Contact</a></li>
            </ul>
        </nav>
    </header>
    
    <main>
        <section id="home">
            <h2>Home Section</h2>
            <p>This is the home section content.</p>
        </section>
        
        <section id="about">
            <h2>About Section</h2>
            <p>This is the about section content.</p>
        </section>
        
        <section id="contact">
            <h2>Contact Section</h2>
            <p>This is the contact section content.</p>
        </section>
    </main>
    
    <footer>
        <p>&copy; 2024 My Project. All rights reserved.</p>
    </footer>
    
    <script src="script.js"></script>
</body>
</html>
```

### Basic CSS Styling

```css
/* Reset and base styles */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    line-height: 1.6;
    color: #333;
    background-color: #f4f4f4;
}

/* Header styles */
header {
    background-color: #2c3e50;
    color: white;
    padding: 1rem 0;
    position: fixed;
    top: 0;
    width: 100%;
    z-index: 1000;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

header h1 {
    text-align: center;
    margin-bottom: 1rem;
}

nav ul {
    list-style: none;
    display: flex;
    justify-content: center;
    gap: 2rem;
}

nav a {
    color: white;
    text-decoration: none;
    padding: 0.5rem 1rem;
    border-radius: 4px;
    transition: background-color 0.3s ease;
}

nav a:hover {
    background-color: rgba(255,255,255,0.1);
}

/* Main content */
main {
    margin-top: 120px;
    padding: 2rem;
    max-width: 1200px;
    margin-left: auto;
    margin-right: auto;
}

section {
    background: white;
    margin-bottom: 2rem;
    padding: 2rem;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

section h2 {
    color: #2c3e50;
    margin-bottom: 1rem;
    border-bottom: 2px solid #3498db;
    padding-bottom: 0.5rem;
}

/* Footer */
footer {
    background-color: #34495e;
    color: white;
    text-align: center;
    padding: 2rem;
    margin-top: 2rem;
}

/* Responsive design */
@media (max-width: 768px) {
    nav ul {
        flex-direction: column;
        gap: 0.5rem;
    }
    
    main {
        margin-top: 180px;
        padding: 1rem;
    }
    
    section {
        padding: 1rem;
    }
}
```

### Basic JavaScript Functionality

```javascript
// DOM Content Loaded
document.addEventListener('DOMContentLoaded', function() {
    console.log('Page loaded successfully');
    
    // Initialize components
    initNavigation();
    initScrollEffects();
    initFormValidation();
});

// Navigation functionality
function initNavigation() {
    const navLinks = document.querySelectorAll('nav a[href^="#"]');
    
    navLinks.forEach(link => {
        link.addEventListener('click', function(e) {
            e.preventDefault();
            
            const targetId = this.getAttribute('href').substring(1);
            const targetElement = document.getElementById(targetId);
            
            if (targetElement) {
                const headerHeight = document.querySelector('header').offsetHeight;
                const targetPosition = targetElement.offsetTop - headerHeight - 20;
                
                window.scrollTo({
                    top: targetPosition,
                    behavior: 'smooth'
                });
            }
        });
    });
}

// Scroll effects
function initScrollEffects() {
    const sections = document.querySelectorAll('section');
    
    const observerOptions = {
        threshold: 0.1,
        rootMargin: '0px 0px -100px 0px'
    };
    
    const observer = new IntersectionObserver(function(entries) {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.style.opacity = '1';
                entry.target.style.transform = 'translateY(0)';
            }
        });
    }, observerOptions);
    
    sections.forEach(section => {
        section.style.opacity = '0';
        section.style.transform = 'translateY(20px)';
        section.style.transition = 'opacity 0.6s ease, transform 0.6s ease';
        observer.observe(section);
    });
}

// Form validation example
function initFormValidation() {
    const forms = document.querySelectorAll('form');
    
    forms.forEach(form => {
        form.addEventListener('submit', function(e) {
            e.preventDefault();
            
            const formData = new FormData(form);
            const data = Object.fromEntries(formData);
            
            if (validateForm(data)) {
                console.log('Form is valid:', data);
                // Handle form submission
                submitForm(data);
            } else {
                console.log('Form validation failed');
            }
        });
    });
}

function validateForm(data) {
    let isValid = true;
    
    // Email validation
    if (data.email && !isValidEmail(data.email)) {
        showError('email', 'Please enter a valid email address');
        isValid = false;
    }
    
    // Required field validation
    const requiredFields = ['name', 'email'];
    requiredFields.forEach(field => {
        if (!data[field] || data[field].trim() === '') {
            showError(field, `${field} is required`);
            isValid = false;
        }
    });
    
    return isValid;
}

function isValidEmail(email) {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return emailRegex.test(email);
}

function showError(fieldName, message) {
    const field = document.querySelector(`[name="${fieldName}"]`);
    if (field) {
        // Remove existing error
        const existingError = field.parentNode.querySelector('.error-message');
        if (existingError) {
            existingError.remove();
        }
        
        // Add new error
        const errorElement = document.createElement('div');
        errorElement.className = 'error-message';
        errorElement.textContent = message;
        errorElement.style.color = '#e74c3c';
        errorElement.style.fontSize = '0.875rem';
        errorElement.style.marginTop = '0.25rem';
        
        field.parentNode.appendChild(errorElement);
        field.style.borderColor = '#e74c3c';
    }
}

async function submitForm(data) {
    try {
        const response = await fetch('/api/submit', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify(data)
        });
        
        if (response.ok) {
            const result = await response.json();
            console.log('Form submitted successfully:', result);
            showSuccessMessage('Form submitted successfully!');
        } else {
            throw new Error('Failed to submit form');
        }
    } catch (error) {
        console.error('Error submitting form:', error);
        showErrorMessage('Failed to submit form. Please try again.');
    }
}

function showSuccessMessage(message) {
    showNotification(message, 'success');
}

function showErrorMessage(message) {
    showNotification(message, 'error');
}

function showNotification(message, type) {
    const notification = document.createElement('div');
    notification.className = `notification notification--${type}`;
    notification.textContent = message;
    
    // Styling
    notification.style.position = 'fixed';
    notification.style.top = '20px';
    notification.style.right = '20px';
    notification.style.padding = '1rem 1.5rem';
    notification.style.borderRadius = '4px';
    notification.style.color = 'white';
    notification.style.fontWeight = 'bold';
    notification.style.zIndex = '10000';
    notification.style.opacity = '0';
    notification.style.transform = 'translateX(100%)';
    notification.style.transition = 'all 0.3s ease';
    
    if (type === 'success') {
        notification.style.backgroundColor = '#27ae60';
    } else {
        notification.style.backgroundColor = '#e74c3c';
    }
    
    document.body.appendChild(notification);
    
    // Animate in
    setTimeout(() => {
        notification.style.opacity = '1';
        notification.style.transform = 'translateX(0)';
    }, 100);
    
    // Remove after 5 seconds
    setTimeout(() => {
        notification.style.opacity = '0';
        notification.style.transform = 'translateX(100%)';
        setTimeout(() => {
            document.body.removeChild(notification);
        }, 300);
    }, 5000);
}

// Utility functions
const utils = {
    // Debounce function
    debounce: function(func, wait) {
        let timeout;
        return function executedFunction(...args) {
            const later = () => {
                clearTimeout(timeout);
                func(...args);
            };
            clearTimeout(timeout);
            timeout = setTimeout(later, wait);
        };
    },
    
    // Throttle function
    throttle: function(func, limit) {
        let inThrottle;
        return function() {
            const args = arguments;
            const context = this;
            if (!inThrottle) {
                func.apply(context, args);
                inThrottle = true;
                setTimeout(() => inThrottle = false, limit);
            }
        };
    },
    
    // Format date
    formatDate: function(date, options = {}) {
        const defaultOptions = {
            year: 'numeric',
            month: 'long',
            day: 'numeric'
        };
        return new Intl.DateTimeFormat('en-US', {...defaultOptions, ...options}).format(date);
    },
    
    // Generate random ID
    generateId: function(length = 8) {
        return Math.random().toString(36).substring(2, length + 2);
    },
    
    // Local storage helpers
    storage: {
        set: function(key, value) {
            try {
                localStorage.setItem(key, JSON.stringify(value));
                return true;
            } catch (error) {
                console.error('Error saving to localStorage:', error);
                return false;
            }
        },
        
        get: function(key, defaultValue = null) {
            try {
                const item = localStorage.getItem(key);
                return item ? JSON.parse(item) : defaultValue;
            } catch (error) {
                console.error('Error reading from localStorage:', error);
                return defaultValue;
            }
        },
        
        remove: function(key) {
            try {
                localStorage.removeItem(key);
                return true;
            } catch (error) {
                console.error('Error removing from localStorage:', error);
                return false;
            }
        }
    }
};
```

## Advanced Examples

### React Component with Hooks

```jsx
import React, { useState, useEffect, useCallback, useMemo } from 'react';

/**
 * Advanced Todo List Component
 * Demonstrates state management, effects, memoization, and event handling
 */
const TodoList = () => {
    const [todos, setTodos] = useState([]);
    const [filter, setFilter] = useState('all');
    const [inputValue, setInputValue] = useState('');
    const [isLoading, setIsLoading] = useState(false);

    // Load todos from API on component mount
    useEffect(() => {
        const loadTodos = async () => {
            setIsLoading(true);
            try {
                const response = await fetch('/api/todos');
                const data = await response.json();
                setTodos(data);
            } catch (error) {
                console.error('Failed to load todos:', error);
            } finally {
                setIsLoading(false);
            }
        };

        loadTodos();
    }, []);

    // Memoized filtered todos
    const filteredTodos = useMemo(() => {
        switch (filter) {
            case 'active':
                return todos.filter(todo => !todo.completed);
            case 'completed':
                return todos.filter(todo => todo.completed);
            default:
                return todos;
        }
    }, [todos, filter]);

    // Memoized statistics
    const stats = useMemo(() => {
        const total = todos.length;
        const completed = todos.filter(todo => todo.completed).length;
        const active = total - completed;
        return { total, completed, active };
    }, [todos]);

    // Add new todo
    const addTodo = useCallback(async (text) => {
        if (!text.trim()) return;

        const newTodo = {
            id: Date.now(),
            text: text.trim(),
            completed: false,
            createdAt: new Date().toISOString()
        };

        try {
            const response = await fetch('/api/todos', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(newTodo)
            });

            if (response.ok) {
                setTodos(prev => [...prev, newTodo]);
                setInputValue('');
            }
        } catch (error) {
            console.error('Failed to add todo:', error);
        }
    }, []);

    // Toggle todo completion
    const toggleTodo = useCallback(async (id) => {
        const todo = todos.find(t => t.id === id);
        if (!todo) return;

        const updatedTodo = { ...todo, completed: !todo.completed };

        try {
            const response = await fetch(`/api/todos/${id}`, {
                method: 'PUT',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(updatedTodo)
            });

            if (response.ok) {
                setTodos(prev => prev.map(t => t.id === id ? updatedTodo : t));
            }
        } catch (error) {
            console.error('Failed to update todo:', error);
        }
    }, [todos]);

    // Delete todo
    const deleteTodo = useCallback(async (id) => {
        try {
            const response = await fetch(`/api/todos/${id}`, {
                method: 'DELETE'
            });

            if (response.ok) {
                setTodos(prev => prev.filter(t => t.id !== id));
            }
        } catch (error) {
            console.error('Failed to delete todo:', error);
        }
    }, []);

    // Handle form submission
    const handleSubmit = useCallback((e) => {
        e.preventDefault();
        addTodo(inputValue);
    }, [inputValue, addTodo]);

    // Handle input change
    const handleInputChange = useCallback((e) => {
        setInputValue(e.target.value);
    }, []);

    if (isLoading) {
        return <div className="loading">Loading todos...</div>;
    }

    return (
        <div className="todo-app">
            <header className="todo-header">
                <h1>Todo List</h1>
                <div className="todo-stats">
                    <span>Total: {stats.total}</span>
                    <span>Active: {stats.active}</span>
                    <span>Completed: {stats.completed}</span>
                </div>
            </header>

            <form onSubmit={handleSubmit} className="todo-form">
                <input
                    type="text"
                    value={inputValue}
                    onChange={handleInputChange}
                    placeholder="Add a new todo..."
                    className="todo-input"
                />
                <button type="submit" className="todo-submit">
                    Add Todo
                </button>
            </form>

            <div className="todo-filters">
                <button
                    className={filter === 'all' ? 'active' : ''}
                    onClick={() => setFilter('all')}
                >
                    All
                </button>
                <button
                    className={filter === 'active' ? 'active' : ''}
                    onClick={() => setFilter('active')}
                >
                    Active
                </button>
                <button
                    className={filter === 'completed' ? 'active' : ''}
                    onClick={() => setFilter('completed')}
                >
                    Completed
                </button>
            </div>

            <ul className="todo-list">
                {filteredTodos.map(todo => (
                    <li key={todo.id} className={`todo-item ${todo.completed ? 'completed' : ''}`}>
                        <input
                            type="checkbox"
                            checked={todo.completed}
                            onChange={() => toggleTodo(todo.id)}
                            className="todo-checkbox"
                        />
                        <span className="todo-text">{todo.text}</span>
                        <button
                            onClick={() => deleteTodo(todo.id)}
                            className="todo-delete"
                            aria-label="Delete todo"
                        >
                            ×
                        </button>
                    </li>
                ))}
            </ul>

            {filteredTodos.length === 0 && (
                <div className="empty-state">
                    {filter === 'all' ? 'No todos yet' : `No ${filter} todos`}
                </div>
            )}
        </div>
    );
};

export default TodoList;
```

### Node.js API Example

```javascript
const express = require('express');
const cors = require('cors');
const helmet = require('helmet');
const rateLimit = require('express-rate-limit');
const { body, validationResult } = require('express-validator');

const app = express();
const PORT = process.env.PORT || 3000;

// Middleware
app.use(helmet());
app.use(cors());
app.use(express.json({ limit: '10mb' }));
app.use(express.urlencoded({ extended: true }));

// Rate limiting
const limiter = rateLimit({
    windowMs: 15 * 60 * 1000, // 15 minutes
    max: 100, // limit each IP to 100 requests per windowMs
    message: 'Too many requests from this IP, please try again later.'
});
app.use('/api/', limiter);

// In-memory storage (use database in production)
let todos = [
    { id: 1, text: 'Learn Node.js', completed: false, createdAt: new Date().toISOString() },
    { id: 2, text: 'Build an API', completed: true, createdAt: new Date().toISOString() }
];
let currentId = 2;

// Validation middleware
const todoValidation = [
    body('text')
        .trim()
        .isLength({ min: 1, max: 200 })
        .withMessage('Text must be between 1 and 200 characters'),
    body('completed')
        .optional()
        .isBoolean()
        .withMessage('Completed must be a boolean')
];

// Error handling middleware
const handleValidationErrors = (req, res, next) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
        return res.status(400).json({
            error: 'Validation failed',
            details: errors.array()
        });
    }
    next();
};

// Routes

/**
 * GET /api/todos
 * Get all todos with optional filtering
 */
app.get('/api/todos', (req, res) => {
    try {
        const { completed, limit = 50, offset = 0 } = req.query;
        
        let filteredTodos = todos;
        
        // Filter by completion status
        if (completed !== undefined) {
            const isCompleted = completed === 'true';
            filteredTodos = todos.filter(todo => todo.completed === isCompleted);
        }
        
        // Pagination
        const startIndex = parseInt(offset);
        const endIndex = startIndex + parseInt(limit);
        const paginatedTodos = filteredTodos.slice(startIndex, endIndex);
        
        res.json({
            todos: paginatedTodos,
            total: filteredTodos.length,
            offset: parseInt(offset),
            limit: parseInt(limit)
        });
    } catch (error) {
        console.error('Error fetching todos:', error);
        res.status(500).json({ error: 'Internal server error' });
    }
});

/**
 * GET /api/todos/:id
 * Get a specific todo by ID
 */
app.get('/api/todos/:id', (req, res) => {
    try {
        const id = parseInt(req.params.id);
        const todo = todos.find(t => t.id === id);
        
        if (!todo) {
            return res.status(404).json({ error: 'Todo not found' });
        }
        
        res.json(todo);
    } catch (error) {
        console.error('Error fetching todo:', error);
        res.status(500).json({ error: 'Internal server error' });
    }
});

/**
 * POST /api/todos
 * Create a new todo
 */
app.post('/api/todos', todoValidation, handleValidationErrors, (req, res) => {
    try {
        const { text, completed = false } = req.body;
        
        const newTodo = {
            id: ++currentId,
            text,
            completed,
            createdAt: new Date().toISOString(),
            updatedAt: new Date().toISOString()
        };
        
        todos.push(newTodo);
        
        res.status(201).json(newTodo);
    } catch (error) {
        console.error('Error creating todo:', error);
        res.status(500).json({ error: 'Internal server error' });
    }
});

/**
 * PUT /api/todos/:id
 * Update a specific todo
 */
app.put('/api/todos/:id', todoValidation, handleValidationErrors, (req, res) => {
    try {
        const id = parseInt(req.params.id);
        const todoIndex = todos.findIndex(t => t.id === id);
        
        if (todoIndex === -1) {
            return res.status(404).json({ error: 'Todo not found' });
        }
        
        const { text, completed } = req.body;
        
        todos[todoIndex] = {
            ...todos[todoIndex],
            text: text !== undefined ? text : todos[todoIndex].text,
            completed: completed !== undefined ? completed : todos[todoIndex].completed,
            updatedAt: new Date().toISOString()
        };
        
        res.json(todos[todoIndex]);
    } catch (error) {
        console.error('Error updating todo:', error);
        res.status(500).json({ error: 'Internal server error' });
    }
});

/**
 * DELETE /api/todos/:id
 * Delete a specific todo
 */
app.delete('/api/todos/:id', (req, res) => {
    try {
        const id = parseInt(req.params.id);
        const todoIndex = todos.findIndex(t => t.id === id);
        
        if (todoIndex === -1) {
            return res.status(404).json({ error: 'Todo not found' });
        }
        
        const deletedTodo = todos.splice(todoIndex, 1)[0];
        
        res.json({ message: 'Todo deleted successfully', todo: deletedTodo });
    } catch (error) {
        console.error('Error deleting todo:', error);
        res.status(500).json({ error: 'Internal server error' });
    }
});

/**
 * GET /api/health
 * Health check endpoint
 */
app.get('/api/health', (req, res) => {
    res.json({
        status: 'OK',
        timestamp: new Date().toISOString(),
        uptime: process.uptime(),
        version: process.env.npm_package_version || '1.0.0'
    });
});

// Global error handler
app.use((error, req, res, next) => {
    console.error('Unhandled error:', error);
    res.status(500).json({ error: 'Internal server error' });
});

// 404 handler
app.use((req, res) => {
    res.status(404).json({ error: 'Endpoint not found' });
});

// Start server
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
    console.log(`Health check: http://localhost:${PORT}/api/health`);
});

module.exports = app;
```

## Testing Examples

### Jest Unit Tests

```javascript
// utils.test.js
const { 
    debounce, 
    throttle, 
    formatDate, 
    generateId, 
    storage 
} = require('./utils');

describe('Utility Functions', () => {
    beforeEach(() => {
        jest.clearAllMocks();
        localStorage.clear();
    });

    describe('debounce', () => {
        test('should delay function execution', (done) => {
            const mockFn = jest.fn();
            const debouncedFn = debounce(mockFn, 100);

            debouncedFn();
            debouncedFn();
            debouncedFn();

            expect(mockFn).not.toHaveBeenCalled();

            setTimeout(() => {
                expect(mockFn).toHaveBeenCalledTimes(1);
                done();
            }, 150);
        });

        test('should pass arguments to debounced function', (done) => {
            const mockFn = jest.fn();
            const debouncedFn = debounce(mockFn, 50);

            debouncedFn('arg1', 'arg2');

            setTimeout(() => {
                expect(mockFn).toHaveBeenCalledWith('arg1', 'arg2');
                done();
            }, 100);
        });
    });

    describe('storage', () => {
        test('should save and retrieve data', () => {
            const testData = { name: 'John', age: 30 };
            
            expect(storage.set('user', testData)).toBe(true);
            expect(storage.get('user')).toEqual(testData);
        });

        test('should return default value for non-existent key', () => {
            expect(storage.get('nonexistent', 'default')).toBe('default');
        });

        test('should remove data', () => {
            storage.set('temp', 'value');
            expect(storage.remove('temp')).toBe(true);
            expect(storage.get('temp')).toBe(null);
        });
    });

    describe('generateId', () => {
        test('should generate ID of specified length', () => {
            const id = generateId(10);
            expect(id).toHaveLength(10);
            expect(typeof id).toBe('string');
        });

        test('should generate unique IDs', () => {
            const id1 = generateId();
            const id2 = generateId();
            expect(id1).not.toBe(id2);
        });
    });
});
```

### React Testing Library Examples

```javascript
// TodoList.test.js
import React from 'react';
import { render, screen, fireEvent, waitFor } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import TodoList from './TodoList';

// Mock fetch
global.fetch = jest.fn();

describe('TodoList Component', () => {
    beforeEach(() => {
        fetch.mockClear();
    });

    test('renders todo list with initial data', async () => {
        const mockTodos = [
            { id: 1, text: 'Test todo', completed: false, createdAt: '2024-01-01' }
        ];

        fetch.mockResolvedValueOnce({
            ok: true,
            json: async () => mockTodos
        });

        render(<TodoList />);

        expect(screen.getByText('Loading todos...')).toBeInTheDocument();

        await waitFor(() => {
            expect(screen.getByText('Test todo')).toBeInTheDocument();
        });

        expect(screen.getByText('Total: 1')).toBeInTheDocument();
        expect(screen.getByText('Active: 1')).toBeInTheDocument();
        expect(screen.getByText('Completed: 0')).toBeInTheDocument();
    });

    test('adds new todo when form is submitted', async () => {
        const user = userEvent.setup();
        
        fetch
            .mockResolvedValueOnce({ ok: true, json: async () => [] }) // Initial load
            .mockResolvedValueOnce({ ok: true, json: async () => ({}) }); // Add todo

        render(<TodoList />);

        await waitFor(() => {
            expect(screen.queryByText('Loading todos...')).not.toBeInTheDocument();
        });

        const input = screen.getByPlaceholderText('Add a new todo...');
        const submitButton = screen.getByText('Add Todo');

        await user.type(input, 'New todo item');
        await user.click(submitButton);

        expect(fetch).toHaveBeenCalledWith('/api/todos', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({
                id: expect.any(Number),
                text: 'New todo item',
                completed: false,
                createdAt: expect.any(String)
            })
        });
    });

    test('toggles todo completion when checkbox is clicked', async () => {
        const mockTodos = [
            { id: 1, text: 'Test todo', completed: false, createdAt: '2024-01-01' }
        ];

        fetch
            .mockResolvedValueOnce({ ok: true, json: async () => mockTodos })
            .mockResolvedValueOnce({ ok: true, json: async () => ({}) });

        render(<TodoList />);

        await waitFor(() => {
            expect(screen.getByText('Test todo')).toBeInTheDocument();
        });

        const checkbox = screen.getByRole('checkbox');
        fireEvent.click(checkbox);

        expect(fetch).toHaveBeenCalledWith('/api/todos/1', {
            method: 'PUT',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({
                id: 1,
                text: 'Test todo',
                completed: true,
                createdAt: '2024-01-01'
            })
        });
    });

    test('filters todos correctly', async () => {
        const mockTodos = [
            { id: 1, text: 'Active todo', completed: false, createdAt: '2024-01-01' },
            { id: 2, text: 'Completed todo', completed: true, createdAt: '2024-01-01' }
        ];

        fetch.mockResolvedValueOnce({
            ok: true,
            json: async () => mockTodos
        });

        render(<TodoList />);

        await waitFor(() => {
            expect(screen.getByText('Active todo')).toBeInTheDocument();
            expect(screen.getByText('Completed todo')).toBeInTheDocument();
        });

        // Filter active todos
        fireEvent.click(screen.getByText('Active'));
        expect(screen.getByText('Active todo')).toBeInTheDocument();
        expect(screen.queryByText('Completed todo')).not.toBeInTheDocument();

        // Filter completed todos
        fireEvent.click(screen.getByText('Completed'));
        expect(screen.queryByText('Active todo')).not.toBeInTheDocument();
        expect(screen.getByText('Completed todo')).toBeInTheDocument();

        // Show all todos
        fireEvent.click(screen.getByText('All'));
        expect(screen.getByText('Active todo')).toBeInTheDocument();
        expect(screen.getByText('Completed todo')).toBeInTheDocument();
    });
});
```

## Deployment Examples

### GitHub Actions CI/CD

```yaml
# .github/workflows/ci-cd.yml
name: CI/CD Pipeline

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    
    strategy:
      matrix:
        node-version: [16.x, 18.x, 20.x]
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
    
    - name: Install dependencies
      run: npm ci
    
    - name: Run linter
      run: npm run lint
    
    - name: Run tests
      run: npm run test:coverage
    
    - name: Upload coverage to Codecov
      uses: codecov/codecov-action@v3
      with:
        file: ./coverage/lcov.info
        flags: unittests
        name: codecov-umbrella

  build:
    needs: test
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Use Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18.x'
        cache: 'npm'
    
    - name: Install dependencies
      run: npm ci
    
    - name: Build application
      run: npm run build
    
    - name: Upload build artifacts
      uses: actions/upload-artifact@v3
      with:
        name: build-files
        path: dist/

  deploy:
    needs: [test, build]
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Download build artifacts
      uses: actions/download-artifact@v3
      with:
        name: build-files
        path: dist/
    
    - name: Deploy to GitHub Pages
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./dist
```

### Docker Configuration

```dockerfile
# Dockerfile
FROM node:18-alpine AS builder

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm ci --only=production

# Copy source code
COPY . .

# Build application
RUN npm run build

# Production stage
FROM nginx:alpine

# Copy built application
COPY --from=builder /app/dist /usr/share/nginx/html

# Copy nginx configuration
COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

```yaml
# docker-compose.yml
version: '3.8'

services:
  app:
    build: .
    ports:
      - "80:80"
    environment:
      - NODE_ENV=production
    restart: unless-stopped
    
  api:
    build: ./api
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - DATABASE_URL=${DATABASE_URL}
    restart: unless-stopped
    depends_on:
      - database
      
  database:
    image: postgres:15-alpine
    environment:
      - POSTGRES_DB=${DB_NAME}
      - POSTGRES_USER=${DB_USER}
      - POSTGRES_PASSWORD=${DB_PASSWORD}
    volumes:
      - postgres_data:/var/lib/postgresql/data
    restart: unless-stopped

volumes:
  postgres_data:
```

## Performance Optimization Examples

### Web Performance

```javascript
// Performance monitoring
const performanceMonitor = {
    // Measure page load time
    measurePageLoad() {
        window.addEventListener('load', () => {
            const loadTime = performance.timing.loadEventEnd - performance.timing.navigationStart;
            console.log(`Page load time: ${loadTime}ms`);
            
            // Send to analytics
            this.sendMetric('page_load_time', loadTime);
        });
    },
    
    // Measure Core Web Vitals
    measureCoreWebVitals() {
        // Largest Contentful Paint
        new PerformanceObserver((list) => {
            const entries = list.getEntries();
            const lastEntry = entries[entries.length - 1];
            console.log('LCP:', lastEntry.startTime);
            this.sendMetric('lcp', lastEntry.startTime);
        }).observe({ entryTypes: ['largest-contentful-paint'] });
        
        // First Input Delay
        new PerformanceObserver((list) => {
            const entries = list.getEntries();
            entries.forEach(entry => {
                console.log('FID:', entry.processingStart - entry.startTime);
                this.sendMetric('fid', entry.processingStart - entry.startTime);
            });
        }).observe({ entryTypes: ['first-input'] });
        
        // Cumulative Layout Shift
        let clsValue = 0;
        new PerformanceObserver((list) => {
            for (const entry of list.getEntries()) {
                if (!entry.hadRecentInput) {
                    clsValue += entry.value;
                }
            }
            console.log('CLS:', clsValue);
            this.sendMetric('cls', clsValue);
        }).observe({ entryTypes: ['layout-shift'] });
    },
    
    sendMetric(name, value) {
        // Send to your analytics service
        if (window.gtag) {
            gtag('event', name, {
                custom_parameter: value
            });
        }
    }
};

// Initialize performance monitoring
performanceMonitor.measurePageLoad();
performanceMonitor.measureCoreWebVitals();
```

This comprehensive documentation provides templates, examples, and best practices for documenting APIs, components, and functions. The examples cover various technologies and frameworks, making it easy to adapt to different project types and requirements.