# Contributing to Last Chaos Source

Thank you for your interest in contributing to the Last Chaos source code! This document provides guidelines and best practices for contributing to this community-maintained MMORPG project.

## Code of Conduct

- **Be Respectful**: Treat all community members with respect and professionalism
- **Be Collaborative**: Work together to improve the game for everyone
- **Be Patient**: This is a volunteer-driven project; allow time for reviews and responses
- **Share Knowledge**: Help others learn and understand the codebase
- **Preserve Game Balance**: Consider the impact of changes on gameplay experience

## Getting Started

### Prerequisites

#### For Windows Development
- Visual Studio 2010 or later (2019+ recommended)
- Windows SDK
- MySQL development libraries
- DirectX SDK (for client development)
- Git for version control

#### For Linux Server Development
- GCC 4.8+ or Clang 3.5+
- GNU Make
- MySQL development headers (libmysql-dev)
- zlib development libraries
- Git for version control

### Setting Up Your Development Environment

1. **Fork the Repository**
   ```bash
   # Click "Fork" on GitHub, then clone your fork
   git clone https://github.com/yourusername/LCSource.git
   cd LCSource
   git remote add upstream https://github.com/evervibestudios/LCSource.git
   ```

2. **Build Setup**
   ```bash
   # For Windows (Visual Studio)
   # Open Server Source/Server.sln or Client Source/All.sln
   
   # For Linux Server Build
   cd "Server Source"
   make clean && make
   ```

3. **Database Setup**
   ```bash
   # Install MySQL and create development databases
   # Import database schemas from DB Scheme.xls
   # Configure connection settings in server configuration files
   ```

## Contributing Process

### 1. Issue Reporting

Before starting work, check existing issues or create a new one:

- **Bug Reports**: Include detailed reproduction steps, environment info, and error messages
- **Feature Requests**: Describe the proposed functionality and its benefits
- **Security Issues**: Report security vulnerabilities privately to maintainers

### 2. Branching Strategy

Use descriptive branch names following this pattern:
```bash
# Bug fixes
git checkout -b fix/login-server-crash-on-disconnect

# New features  
git checkout -b feature/guild-alliance-system

# Security improvements
git checkout -b security/fix-sql-injection-vulnerability

# Documentation updates
git checkout -b docs/update-build-instructions
```

### 3. Development Guidelines

#### Code Style

**C/C++ Code Standards:**
```cpp
// Use consistent indentation (tabs or 4 spaces)
// Class names: PascalCase
class GameServer {
private:
    // Private members with m_ prefix
    int m_playerCount;
    std::string m_serverName;
    
public:
    // Function names: PascalCase
    void StartServer();
    bool IsRunning() const;
    
    // Constants: ALL_CAPS
    static const int MAX_PLAYERS = 5000;
};

// Variable names: camelCase
int playerLevel = 50;
std::vector<Player*> activePlayers;

// Function parameters: camelCase
void ProcessPlayerLogin(const std::string& userName, int accountId);
```

**Commenting Standards:**
```cpp
/**
 * Brief description of the function
 * @param userName The player's login name
 * @param accountId Unique account identifier
 * @return true if login successful, false otherwise
 */
bool AuthenticatePlayer(const std::string& userName, int accountId);

// Inline comments for complex logic
if (playerLevel >= REBIRTH_MIN_LEVEL) {
    // Allow rebirth only if player meets requirements
    EnableRebirthOption(player);
}
```

#### Security Considerations

**Always consider security implications:**
```cpp
// BAD: Potential buffer overflow
char buffer[256];
strcpy(buffer, userInput);

// GOOD: Safe string handling
std::string buffer = std::string(userInput).substr(0, 255);

// BAD: SQL injection vulnerability
sprintf(query, "SELECT * FROM users WHERE name='%s'", userName);

// GOOD: Use prepared statements
PreparedStatement* stmt = connection->prepareStatement(
    "SELECT * FROM users WHERE name=?");
stmt->setString(1, userName);
```

#### Performance Guidelines

- **Memory Management**: Use RAII and smart pointers where possible
- **Database Access**: Use connection pooling and prepared statements
- **Network Efficiency**: Minimize packet size and frequency
- **Threading**: Use appropriate synchronization for multi-threaded code

### 4. Testing Requirements

#### Code Testing
```cpp
// Include basic validation in your changes
assert(playerLevel >= 0 && playerLevel <= MAX_LEVEL);

// Test edge cases
if (inventory.size() >= MAX_INVENTORY_SIZE) {
    return ERROR_INVENTORY_FULL;
}
```

#### Manual Testing
- **Functionality**: Verify your changes work as intended
- **Regression**: Ensure existing features still work
- **Performance**: Check that changes don't significantly impact performance
- **Security**: Verify no new security vulnerabilities are introduced

### 5. Commit Guidelines

#### Commit Message Format
```
type(scope): brief description

Detailed explanation of changes made, why they were necessary,
and any important implementation details.

Fixes #123
```

#### Commit Types
- **fix**: Bug fixes
- **feat**: New features
- **security**: Security improvements
- **perf**: Performance improvements
- **refactor**: Code refactoring
- **docs**: Documentation changes
- **style**: Code style changes
- **test**: Test additions or modifications

#### Examples
```bash
fix(gameserver): resolve crash when player disconnects during combat

The server was not properly cleaning up combat state when a player
disconnected mid-battle, causing a null pointer dereference.

- Added null checks in CombatManager::ProcessPlayerDisconnect()
- Properly clean up combat timers and effects
- Added logging for debugging similar issues

Fixes #456

feat(guild): add guild alliance system

Implements the ability for guilds to form alliances for coordinated
warfare and shared resources.

- Added Alliance table to database schema
- Implemented alliance invitation and management UI
- Added alliance chat channel
- Updated guild war system to respect alliances

Closes #789
```

### 6. Pull Request Process

#### Creating a Pull Request

1. **Update Your Branch**
   ```bash
   git fetch upstream
   git rebase upstream/master
   ```

2. **Create Pull Request**
   - Use descriptive title summarizing the change
   - Include detailed description of what changed and why
   - Reference related issues
   - Add screenshots for UI changes
   - List any breaking changes

#### Pull Request Template
```markdown
## Description
Brief description of changes made.

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Security improvement
- [ ] Performance improvement
- [ ] Documentation update

## Testing
- [ ] Manual testing completed
- [ ] No regression issues found
- [ ] Performance impact assessed

## Security Review
- [ ] No new security vulnerabilities introduced
- [ ] Input validation implemented where applicable
- [ ] Authentication/authorization respected

## Related Issues
Fixes #123
Closes #456

## Screenshots (if applicable)
[Include screenshots for UI changes]
```

### 7. Code Review Process

#### For Contributors
- **Be Patient**: Reviews take time; maintainers are volunteers
- **Be Responsive**: Address review feedback promptly
- **Ask Questions**: If feedback is unclear, ask for clarification
- **Learn**: Use reviews as learning opportunities

#### Review Criteria
Reviewers will evaluate:
- **Functionality**: Does the code work as intended?
- **Security**: Are there any security implications?
- **Performance**: Does it impact game performance?
- **Code Quality**: Is the code maintainable and well-structured?
- **Compatibility**: Does it break existing functionality?

## Specialized Contributing Areas

### Client Development
- **Graphics**: DirectX/OpenGL rendering improvements
- **UI/UX**: User interface enhancements
- **Performance**: Client-side optimization
- **Compatibility**: Cross-platform support

### Server Development
- **Game Logic**: Combat, skills, quests, and game mechanics
- **Database**: Schema improvements and query optimization
- **Networking**: Protocol enhancements and security
- **Scalability**: Performance and capacity improvements

### Infrastructure
- **Build Systems**: Compilation and deployment improvements
- **Documentation**: Technical documentation and guides
- **Testing**: Automated testing and quality assurance
- **Security**: Vulnerability assessment and remediation

## Community Guidelines

### Communication Channels
- **GitHub Issues**: Bug reports and feature requests
- **GitHub Discussions**: General development discussion
- **Pull Request Comments**: Code-specific discussions

### Getting Help
- **Documentation**: Check existing documentation first
- **Search**: Search existing issues and discussions
- **Ask Questions**: Create new issues for questions
- **Be Specific**: Provide detailed context and examples

### Recognition
Contributors will be recognized through:
- **Git History**: All contributions are permanently recorded
- **Release Notes**: Significant contributions mentioned in releases
- **Community Recognition**: Outstanding contributors highlighted

## Legal Considerations

### Licensing
- All contributions must be compatible with the project license
- Contributors grant rights to use their contributions
- Respect original intellectual property rights

### Copyright
- Don't copy code from other projects without proper licensing
- Ensure you have rights to contribute any code you submit
- Respect third-party library licenses and attributions

## Release Process

### Versioning
- **Major**: Significant feature additions or breaking changes
- **Minor**: New features and improvements
- **Patch**: Bug fixes and security updates

### Release Cycle
- Regular maintenance releases for bug fixes
- Feature releases when significant improvements are ready
- Security releases as needed for critical vulnerabilities

## Conclusion

Contributing to Last Chaos helps preserve and improve this classic MMORPG for the community. Whether you're fixing bugs, adding features, improving security, or updating documentation, your contributions make a difference.

Remember that this is a collaborative effort, and we're all working together to maintain and enhance this game. Be patient, respectful, and helpful to create a positive development environment for everyone.

Thank you for contributing to Last Chaos!