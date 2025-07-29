# 🤝 Contributing to Redox Client

Thank you for your interest in contributing to Redox Client! We welcome contributions from developers of all skill levels. This guide will help you get started with contributing to our project.

## 📋 Table of Contents

- [🎯 Getting Started](#-getting-started)
- [🔧 Development Setup](#-development-setup)
- [📝 Contribution Types](#-contribution-types)
- [🏗️ Code Guidelines](#️-code-guidelines)
- [🧪 Testing](#-testing)
- [📤 Submitting Changes](#-submitting-changes)
- [🎨 Design Guidelines](#-design-guidelines)
- [🐛 Bug Reports](#-bug-reports)
- [💡 Feature Requests](#-feature-requests)
- [👥 Community](#-community)

---

## 🎯 Getting Started

### Prerequisites

Before contributing, ensure you have:

- **Java Development Kit 17+** (We recommend Java 21)
- **IntelliJ IDEA** or **Eclipse IDE** (IntelliJ preferred)
- **Git** for version control
- **Gradle** 8.0+ (included with project wrapper)
- **Minecraft Development Kit (MDK)** for your target version

### 🍴 Fork & Clone

1. **Fork** the repository on GitHub
2. **Clone** your fork locally:
   ```bash
   git clone https://github.com/YOUR_USERNAME/redox.git
   cd redox
   ```
3. **Add upstream** remote:
   ```bash
   git remote add upstream https://github.com/sk1dd3d/redox.git
   ```

---

## 🔧 Development Setup

### IDE Configuration

**For IntelliJ IDEA:**

1. **Open** the project in IntelliJ IDEA
2. **Import** Gradle project when prompted
3. **Configure** JDK to Java 17+
4. **Install** recommended plugins:
   - Minecraft Development for IntelliJ
   - GitToolBox
   - Rainbow Brackets
   - CodeGlance Pro

**Build Configuration:**
```bash
# Generate development environment
./gradlew genEclipseRuns genIntellijRuns

# Build the project
./gradlew build

# Run Minecraft client with mod
./gradlew runClient
```

---

## 📝 Contribution Types

### 🔧 Code Contributions

- **New Modules**: Implement new cheat modules
- **Bug Fixes**: Fix existing issues
- **Performance**: Optimize existing code
- **Bypasses**: Improve anti-cheat evasion
- **UI/UX**: Enhance user interface

### 📚 Documentation

- **Code Documentation**: Improve inline comments
- **Wiki Pages**: Create user guides
- **API Documentation**: Document public APIs
- **Tutorials**: Write setup/usage guides

### 🐛 Quality Assurance

- **Bug Testing**: Test and report issues
- **Bypass Testing**: Verify anti-cheat evasion
- **Performance Testing**: Profile and optimize
- **Compatibility Testing**: Test across versions

### 🎨 Design & Assets

- **UI Design**: Create interface mockups
- **Icons**: Design module icons
- **Themes**: Create new visual themes
- **Animations**: Implement smooth transitions

---


### 🔒 Security Guidelines

- **Never hardcode** credentials or tokens
- **Validate all inputs** from users
- **Use secure random** for cryptographic operations
- **Minimize permissions** requested
- **Encrypt sensitive data** in configs

### 🚀 Performance Guidelines

- **Avoid unnecessary calculations** in render/update loops
- **Cache expensive operations**
- **Use appropriate data structures**
- **Profile performance-critical code**
- **Minimize memory allocations**

**Example - Efficient Target Finding:**
```java
// ❌ Bad - Recalculates every frame
@EventHandler
public void onUpdate(UpdateEvent event) {
    List<Entity> targets = new ArrayList<>();
    for (Entity entity : mc.world.getEntities()) {
        if (entity instanceof PlayerEntity && mc.player.distanceTo(entity) <= range.getValue()) {
            targets.add(entity);
        }
    }
}

// ✅ Good - Cached with periodic updates
private List<Entity> cachedTargets = new ArrayList<>();
private long lastTargetUpdate = 0;

@EventHandler
public void onUpdate(UpdateEvent event) {
    if (System.currentTimeMillis() - lastTargetUpdate > 100) { // Update every 100ms
        updateTargetCache();
        lastTargetUpdate = System.currentTimeMillis();
    }
}
```

---

## 🧪 Testing

### 🔍 Test Requirements

All contributions must include:

- **Unit tests** for utility functions
- **Integration tests** for module functionality
- **Manual testing** on target servers
- **Performance benchmarks** for critical paths

### 🧪 Testing Framework

```java
// Example test class
public class KillAuraModuleTest {
    
    @Test
    public void testTargetValidation() {
        KillAuraModule killAura = new KillAuraModule();
        // Test logic here
        assertTrue(killAura.isValidTarget(mockPlayer));
    }
    
    @Test
    public void testRangeCalculation() {
        KillAuraModule killAura = new KillAuraModule();
        killAura.range.setValue(4);
        // Test range calculations
        assertEquals(4.0, killAura.getEffectiveRange(), 0.1);
    }
}
```

### 🎮 Manual Testing Checklist

Before submitting:

- [ ] Module enables/disables without errors
- [ ] Settings save and load correctly
- [ ] No console errors or warnings
- [ ] Performance impact is acceptable
- [ ] Works on target Minecraft versions
- [ ] Bypasses work on test servers
- [ ] UI elements display correctly
- [ ] Keybinds function properly

---

## 📤 Submitting Changes

### 🌿 Branch Naming

Use descriptive branch names:

```bash
# Feature branches
feature/killaura-improvements
feature/new-scaffold-mode
feature/gui-redesign

# Bug fix branches
fix/crash-on-disconnect
fix/config-not-saving
fix/memory-leak

# Documentation branches
docs/contributing-guide
docs/api-reference
```

### 💬 Commit Messages

Follow conventional commit format:

```bash
# Format: type(scope): description
feat(combat): add legit mode to killaura
fix(gui): resolve crash when opening settings
docs(readme): update installation instructions
perf(render): optimize ESP rendering
refactor(utils): simplify packet utilities

# Types: feat, fix, docs, style, refactor, perf, test, chore
```

### 🔄 Pull Request Process

1. **Update** your branch with latest upstream:
   ```bash
   git fetch upstream
   git rebase upstream/main
   ```

2. **Create** a pull request with:
   - Clear title and description
   - Reference to related issues
   - Screenshots/videos for UI changes
   - Testing evidence

3. **PR Template**:
   ```markdown
   ## 🎯 Description
   Brief description of changes made.
   
   ## 📋 Type of Change
   - [ ] Bug fix
   - [ ] New feature
   - [ ] Breaking change
   - [ ] Documentation update
   
   ## 🧪 Testing
   - [ ] Manual testing completed
   - [ ] Unit tests added/updated
   - [ ] Performance impact assessed
   
   ## 📸 Screenshots
   (If applicable)
   
   ## 🔗 Related Issues
   Closes #123
   ```

---

## 🎨 Design Guidelines

### 🖌️ UI Design Principles

- **Consistency**: Maintain visual consistency across components
- **Accessibility**: Ensure readable fonts and sufficient contrast
- **Responsiveness**: Support different screen sizes
- **Performance**: Minimize render calls and GPU usage

### 🎨 Color Palette

```java
// Primary colors
public static final Color PRIMARY = new Color(255, 107, 107);      // #ff6b6b
public static final Color SECONDARY = new Color(74, 144, 226);     // #4a90e2
public static final Color SUCCESS = new Color(92, 184, 92);        // #5cb85c
public static final Color WARNING = new Color(240, 173, 78);       // #f0ad4e
public static final Color DANGER = new Color(217, 83, 79);         // #d9534f

// Neutral colors
public static final Color DARK = new Color(44, 44, 44);            // #2c2c2c
public static final Color LIGHT = new Color(248, 249, 250);        // #f8f9fa
public static final Color MUTED = new Color(108, 117, 125);        // #6c757d
```

---

## 🐛 Bug Reports

### 📝 Bug Report Template

When reporting bugs, include:

```markdown
## 🐛 Bug Description
A clear description of what the bug is.

## 🔄 Reproduction Steps
1. Go to '...'
2. Click on '...'
3. Scroll down to '...'
4. See error

## 🎯 Expected Behavior
What you expected to happen.

## 📸 Screenshots/Videos
If applicable, add screenshots or videos.

## 🖥️ Environment
- **OS**: Windows 10/11, macOS, Linux
- **Minecraft Version**: 1.20.1
- **Redox Version**: v2.1.0-indev
- **Java Version**: Java 21
- **Launcher**: Official/MultiMC/PolyMC
- **Other Mods**: List other installed mods

## 📋 Additional Context
Any other relevant information.

## 🔍 Debug Information
```
[Paste relevant log files here]
```
```

### 🚨 Priority Levels

- **🔴 Critical**: Crashes, data loss, security issues
- **🟠 High**: Major functionality broken
- **🟡 Medium**: Minor feature issues
- **🟢 Low**: Cosmetic issues, enhancements

---

## 💡 Feature Requests

### 📋 Feature Request Template

```markdown
## 💡 Feature Description
A clear description of the feature you'd like to see.

## 🎯 Problem Statement
What problem does this feature solve?

## 💭 Proposed Solution
How do you envision this feature working?

## 🔄 Alternative Solutions
Other approaches you've considered.

## 📊 Use Cases
- Use case 1: ...
- Use case 2: ...
- Use case 3: ...

## 🏆 Priority
- [ ] Critical (Must have)
- [ ] High (Should have)
- [ ] Medium (Could have)
- [ ] Low (Nice to have)

## 📸 Mockups/Examples
Visual examples if applicable.
```

### 🎯 Feature Development Process

1. **Discussion**: Feature requests are discussed in Discord/GitHub
2. **Planning**: Technical approach and implementation plan
3. **Development**: Code implementation with tests
4. **Review**: Code review and testing
5. **Release**: Feature included in next release

---

## 👥 Community

### 💬 Communication Channels

- **Discord**: Primary community hub - [Join here](https://discord.gg/redoxclient)
- **GitHub Issues**: Bug reports and feature requests
- **GitHub Discussions**: General questions and ideas
- **Reddit**: r/RedoxClient for community posts

### 🏆 Recognition

Contributors are recognized through:

- **Contributors page** on README
- **Discord roles** for active contributors
- **Credits** in client about section
- **Special mentions** in release notes

### 📋 Contributor Roles

| Role | Requirements | Permissions |
|------|-------------|-------------|
| **Contributor** | 1+ merged PR | Basic GitHub access |
| **Regular Contributor** | 5+ merged PRs | Issue triage |
| **Core Contributor** | 20+ merged PRs | PR review access |
| **Maintainer** | Appointed by team | Repository admin |

---

## 📚 Resources

### 🔗 Useful Links

- **Minecraft Development**: [Fabric Wiki](https://fabricmc.net/wiki/)
- **Mixin Documentation**: [Mixin Docs](https://github.com/SpongePowered/Mixin/wiki)
- **Java Style Guide**: [Google Java Style](https://google.github.io/styleguide/javaguide.html)
- **Git Best Practices**: [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)

### 📖 Learning Resources

**For New Contributors:**
- [Minecraft Modding Tutorial](https://fabricmc.net/wiki/tutorial:setup)
- [Java Programming Basics](https://docs.oracle.com/javase/tutorial/)
- [Git Version Control](https://git-scm.com/book)

**For Advanced Development:**
- [Mixin Advanced Topics](https://github.com/SpongePowered/Mixin/wiki/Advanced-Topics)
- [Minecraft Protocol Documentation](https://wiki.vg/Protocol)
- [Performance Optimization Guide](https://github.com/fabric-community/wiki/wiki/Performance)

### 🛠️ Development Tools

**Recommended Tools:**
- **IDE**: IntelliJ IDEA Ultimate (free for students)
- **Profiler**: JProfiler or VisualVM
- **Decompiler**: Fernflower (built into IntelliJ)
- **Packet Analysis**: PacketLogger mod
- **Performance**: JMH for benchmarking

---

## 🎖️ Code of Conduct

### 🤝 Our Standards

We are committed to providing a welcoming and inspiring community for all. Everyone participating in the Redox Client project is required to abide by our Code of Conduct.

**Positive behaviors include:**
- Using welcoming and inclusive language
- Being respectful of differing viewpoints
- Gracefully accepting constructive criticism
- Focusing on what is best for the community
- Showing empathy towards other community members

**Unacceptable behaviors include:**
- Harassment of any kind
- Discriminatory language or actions
- Personal attacks or insults
- Public or private harassment
- Publishing private information without consent
- Any conduct that could reasonably be considered inappropriate

### 🚨 Enforcement

Instances of abusive, harassing, or otherwise unacceptable behavior may be reported by contacting the project team at redoxsupport@proton.me. All complaints will be reviewed and investigated promptly and fairly.

**Consequences may include:**
- Warning
- Temporary ban from community spaces
- Permanent ban from community spaces
- Removal from contributor status

---

## 📜 Legal Considerations

### ⚖️ Licensing

By contributing to Redox Client, you agree that your contributions will be licensed under the GPL-3.0 license.

### 📋 Contributor License Agreement

All contributors must agree to our Contributor License Agreement (CLA):

- You grant us the right to use your contribution
- You confirm you have the right to make the contribution
- Your contribution is provided "as is" without warranties

### 🔒 Security

If you discover a security vulnerability, please report it privately to security@redoxclient.com instead of creating a public issue.

---

## 🎉 Getting Started Checklist

Ready to contribute? Here's your checklist:

- [ ] Read this contributing guide completely
- [ ] Join our Discord community
- [ ] Set up your development environment
- [ ] Fork and clone the repository
- [ ] Find a good first issue or create a feature proposal
- [ ] Make your changes following our guidelines
- [ ] Test your changes thoroughly
- [ ] Submit a pull request with a clear description
- [ ] Respond to code review feedback
- [ ] Celebrate your contribution! 🎉

---

## ❓ Questions?

If you have any questions about contributing, feel free to:

- Ask in our [Discord server](https://discord.gg/redoxclient)
- Create a [GitHub Discussion](https://github.com/sk1dd3d/redox/discussions)

---

Thank you for contributing to Redox Client! Every contribution, no matter how small, helps make our project better for everyone. 

**Happy coding!** 🚀

---

*This contributing guide is a living document and will be updated as our project evolves. Last updated: January 2025*
