# User Stories Standards

A comprehensive guide for creating effective user stories that drive development, ensure user value, and facilitate team collaboration.

## 🎯 Purpose

User stories serve as the foundation of agile development by:

- **User-Centric Development**: Focusing on user needs and value
- **Communication**: Bridging the gap between stakeholders and developers
- **Planning**: Enabling effective sprint planning and estimation
- **Quality Assurance**: Ensuring delivered features meet user expectations
- **Documentation**: Creating a living record of requirements

## 📋 User Story Structure

### Standard Format

```
As a [user role], I want to [action/feature] so that [benefit/value].
```

### Components Breakdown

| Component          | Description          | Example                                       |
| ------------------ | -------------------- | --------------------------------------------- |
| **User Role**      | Who the story is for | "As a project manager"                        |
| **Action/Feature** | What they want to do | "I want to assign tasks to team members"      |
| **Benefit/Value**  | Why they want it     | "so that work can be distributed effectively" |

## 🏷️ Story Types

### Feature Stories

**Purpose**: New functionality that provides value to users

**Structure**:

```markdown
**Title**: As a [user role], I should be able to [action] so that [benefit]

**Description**:
Detailed description of the story including:

- User scenario and context
- Acceptance criteria
- Business value
- Technical considerations

**Acceptance Criteria**:

- [ ] Criterion 1: Specific, testable requirement
- [ ] Criterion 2: Another testable requirement
- [ ] Criterion 3: Edge case handling

**Definition of Done**:

- [ ] Feature implemented and tested
- [ ] Documentation updated
- [ ] Code reviewed and approved
- [ ] Deployed to staging environment
```

**Example**:

```markdown
**Title**: As a project manager, I should be able to assign tasks to team members so that work can be distributed effectively.

**Description**:
Project managers need the ability to assign specific tasks to team members to ensure proper workload distribution and accountability. This feature should allow managers to:

- View all available team members
- Select tasks from the backlog
- Assign tasks with due dates and priorities
- Track assignment history
- Reassign tasks when needed

**Acceptance Criteria**:

- [ ] Manager can view list of available team members
- [ ] Manager can select tasks from the project backlog
- [ ] Manager can assign tasks with due dates and priority levels
- [ ] Team members receive notifications when tasks are assigned
- [ ] Manager can reassign tasks to different team members
- [ ] Assignment history is tracked and visible
- [ ] System prevents double-assignment of the same task

**Definition of Done**:

- [ ] Task assignment UI implemented and tested
- [ ] Backend API endpoints created and tested
- [ ] Notification system integrated
- [ ] Database schema updated
- [ ] Unit and integration tests written
- [ ] Documentation updated
- [ ] Code reviewed and approved
- [ ] Feature deployed to staging
```

**Note:** Every story title should include the word 'should' as opposed to 'can'. e.g. It's unclear whether the story "User can delete comment" is a feature or a bug. "User should be able to delete comment" or "User should not be able to delete comment" are much clearer: the former is a feature, the latter a bug.

### Bug Stories

**Purpose**: Issues that need to be resolved to maintain system functionality

**Structure**:

```markdown
**Title**: [Issue description] should [expected behavior]

**Description**:

- What is currently happening?
- What should be happening?
- Impact on users and system

**Steps to Reproduce**:

1. Step 1: Specific action
2. Step 2: Another action
3. Step 3: Expected vs actual result

**Acceptance Criteria**:

- [ ] Issue is resolved
- [ ] No regression in related functionality
- [ ] Performance is not negatively impacted
- [ ] User experience is improved

**Definition of Done**:

- [ ] Root cause identified and fixed
- [ ] Fix tested in all affected scenarios
- [ ] Regression tests pass
- [ ] Fix deployed to production
```

**Example**:

```markdown
**Title**: Dashboard layout should display widgets consistently without spacing issues.

**Description**:
The dashboard currently displays inconsistent widget spacing, causing visual problems and poor user experience. Some rows show proper 2-widget layout while others have unwanted gaps or overlapping elements.

**Steps to Reproduce**:

1. Login to the application dashboard
2. Navigate to the main dashboard view
3. Observe the widget layout across different screen sizes
4. Notice inconsistent spacing between widgets

**Expected Behavior**:

- All rows should display exactly 2 widgets per row
- Consistent spacing between widgets
- Responsive layout that works on all screen sizes

**Actual Behavior**:

- Some rows display unwanted spaces between widgets
- Widgets sometimes overlap on smaller screens
- Inconsistent spacing creates visual clutter

**Acceptance Criteria**:

- [ ] All dashboard rows display exactly 2 widgets
- [ ] Consistent spacing between all widgets
- [ ] Responsive design works on mobile and desktop
- [ ] No visual artifacts or overlapping elements
- [ ] Performance is not degraded

**Definition of Done**:

- [ ] CSS layout issues identified and fixed
- [ ] Responsive design tested on multiple devices
- [ ] Visual regression tests pass
- [ ] Performance impact assessed
- [ ] Fix deployed to production
```

### Chore Stories

**Purpose**: Maintenance tasks that support development but don't provide direct user value

**Structure**:

```markdown
**Title**: [Task description] for [purpose/benefit]

**Description**:

- Why is this needed?
- What problem does it solve?
- How does it help the team?

**Acceptance Criteria**:

- [ ] Specific deliverable 1
- [ ] Specific deliverable 2
- [ ] Verification method

**Definition of Done**:

- [ ] Task completed successfully
- [ ] Documentation updated
- [ ] Team notified of changes
- [ ] No negative impact on existing functionality
```

**Example**:

```markdown
**Title**: Setup CI/CD pipeline for automated testing and deployment.

**Description**:
A stable CI/CD pipeline will improve code quality, reduce manual errors, and enable faster delivery cycles. This setup will automate testing, code quality checks, and deployment processes.

**Acceptance Criteria**:

- [ ] Automated testing runs on every commit
- [ ] Code quality checks are enforced
- [ ] Automated deployment to staging environment
- [ ] Deployment notifications are sent to team
- [ ] Rollback capability is available
- [ ] Pipeline is documented and maintainable

**Definition of Done**:

- [ ] GitHub Actions workflow configured
- [ ] All tests pass in CI environment
- [ ] Code quality gates are working
- [ ] Staging deployment is automated
- [ ] Documentation is updated
- [ ] Team is trained on the new process
```

## 📝 Writing Guidelines

### User Role Guidelines

**Be Specific**: Use specific user roles rather than generic terms

```markdown
✅ As a project manager
✅ As a team lead
✅ As a system administrator
❌ As a user
❌ As someone
❌ As a person
```

**Use Personas**: Reference established user personas

```markdown
✅ As a project manager (Sarah)
✅ As a team lead (Mike)
✅ As a system administrator (Admin)
```

### Action Guidelines

**Use Active Voice**: Describe what the user wants to do

```markdown
✅ I want to assign tasks
✅ I want to track progress
✅ I want to generate reports
❌ I want tasks to be assigned
❌ I want progress to be tracked
```

**Be Specific**: Avoid vague or generic actions

```markdown
✅ I want to assign tasks to team members
✅ I want to track project progress
✅ I want to generate monthly reports
❌ I want to manage things
❌ I want to see information
❌ I want to do stuff
```

### Benefit Guidelines

**Focus on Value**: Explain why the feature is important

```markdown
✅ so that work can be distributed effectively
✅ so that I can monitor project health
✅ so that I can make informed decisions
❌ so that it's easier
❌ so that I can do my job
❌ so that it's better
```

**Be Measurable**: Include quantifiable benefits when possible

```markdown
✅ so that I can reduce task assignment time by 50%
✅ so that I can identify bottlenecks within 24 hours
✅ so that I can improve team productivity by 20%
```

## 🎯 Acceptance Criteria

### Writing Effective Criteria

**Use Given-When-Then Format**:

```markdown
**Given** a project manager is logged in
**When** they navigate to the task assignment page
**Then** they should see a list of available team members
**And** they should be able to select tasks from the backlog
**And** they should be able to assign tasks with due dates
```

**Make Them Testable**:

```markdown
✅ The system should display exactly 2 widgets per row
✅ The user should receive an email notification within 5 minutes
✅ The page should load within 3 seconds
❌ The system should be fast
❌ The user should be notified
❌ The page should work well
```

**Include Edge Cases**:

```markdown
- [ ] System handles empty task list gracefully
- [ ] System prevents assignment of completed tasks
- [ ] System validates due dates are in the future
- [ ] System handles concurrent assignment attempts
```

## 📊 Story Sizing

### Estimation Techniques

**Story Points**: Relative sizing based on complexity

- **1 Point**: Simple, well-understood tasks
- **2 Points**: Small features with minimal complexity
- **3 Points**: Medium features with some complexity
- **5 Points**: Large features with significant complexity
- **8 Points**: Very large features requiring investigation
- **13+ Points**: Epic that should be broken down

**T-Shirt Sizing**: Quick estimation method

- **XS**: 1-2 hours
- **S**: 2-4 hours
- **M**: 4-8 hours
- **L**: 1-2 days
- **XL**: 2-5 days
- **XXL**: 1+ weeks (should be broken down)

### Sizing Guidelines

**Consider These Factors**:

- **Complexity**: How difficult is the implementation?
- **Uncertainty**: How much is unknown?
- **Dependencies**: What external factors are involved?
- **Risk**: What could go wrong?
- **Testing**: How much testing is required?

## 🔄 Story Lifecycle

### Story States

1. **Backlog**: Initial story creation
2. **Refined**: Story is detailed and ready for sprint planning
3. **In Progress**: Story is being worked on
4. **In Review**: Story is being tested and reviewed
5. **Done**: Story is complete and accepted
6. **Rejected**: Story is not needed or invalid

### Story Refinement Process

**Initial Creation**:

- Basic user story format
- High-level acceptance criteria
- Initial estimation

**Refinement**:

- Detailed acceptance criteria
- Technical considerations
- Dependencies identified
- Risks assessed

**Sprint Planning**:

- Final acceptance criteria
- Task breakdown
- Assignment to team members
- Sprint commitment

## 🛠️ Tools and Templates

### Story Templates

**Feature Story Template**:

```markdown
## User Story

**As a** [user role]
**I want** [action/feature]
**So that** [benefit/value]

## Acceptance Criteria

- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

## Definition of Done

- [ ] Feature implemented
- [ ] Tests written and passing
- [ ] Documentation updated
- [ ] Code reviewed
- [ ] Deployed to staging
```

**Bug Story Template**:

```markdown
## Bug Report

**Title**: [Issue description]

## Description

- **Current Behavior**: [What is happening]
- **Expected Behavior**: [What should happen]
- **Impact**: [How this affects users]

## Steps to Reproduce

1. [Step 1]
2. [Step 2]
3. [Step 3]

## Acceptance Criteria

- [ ] Issue is resolved
- [ ] No regression in related functionality
- [ ] Performance is maintained
```

### Story Management Tools

**Project Management Platforms**:

- **Jira**: Comprehensive issue tracking
- **Azure DevOps**: Microsoft's project management
- **Linear**: Modern issue tracking
- **Asana**: Team collaboration
- **Trello**: Simple task management

**Best Practices**:

- Use consistent story templates
- Maintain clear acceptance criteria
- Regular backlog refinement
- Effective prioritization
- Regular retrospectives

## 📈 Metrics and Monitoring

### Story Metrics

**Velocity**: Stories completed per sprint
**Cycle Time**: Time from start to completion
**Lead Time**: Time from creation to completion
**Burndown**: Progress tracking during sprints

### Quality Metrics

**Story Completion Rate**: Percentage of stories completed
**Defect Rate**: Bugs found after story completion
**Rework Rate**: Stories requiring significant changes
**Customer Satisfaction**: User feedback on delivered features

## 🎓 Best Practices

### Do's ✅

- **Write from User Perspective**: Focus on user needs
- **Keep Stories Small**: Aim for 1-2 day completion
- **Be Specific**: Clear, unambiguous requirements
- **Include Acceptance Criteria**: Testable conditions
- **Regular Refinement**: Keep backlog current
- **Collaborative Writing**: Involve the whole team

### Don'ts ❌

- **Don't Be Vague**: Avoid ambiguous language
- **Don't Skip Acceptance Criteria**: Always include testable conditions
- **Don't Make Stories Too Large**: Break down epics
- **Don't Ignore Dependencies**: Identify and manage them
- **Don't Skip User Value**: Every story should provide value
- **Don't Forget Edge Cases**: Consider all scenarios

---

**Note**: This is a living document that should evolve with your team's needs and project requirements. Regular reviews and updates ensure the user story process remains effective and valuable.
