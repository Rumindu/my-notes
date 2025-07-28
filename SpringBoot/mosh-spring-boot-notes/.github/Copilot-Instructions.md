# Copilot Instructions for Mosh Spring Boot Course Notes

## 🎯 Purpose

AI assistance commands specifically designed for creating notes from Mosh's Spring Boot course videos using your preferred simple format.

## 📝 Note Template Structure

````markdown
# [Video Title]

<!-- omit from toc -->

## Table of Contents

- [Main Topic 1](#main-topic-1)
- [Main Topic 2](#main-topic-2)
- [Code Examples](#code-examples)
- [Key Points](#key-points)

## Main Topic 1

- Key point with brief explanation
- Another important concept
- Include diagrams/screenshots when needed
  ![Description](assets/image-name.png)

## Code Examples

```java
// Working code with brief comments
@SpringBootApplication
public class MyApp {
    public static void main(String[] args) {
        SpringApplication.run(MyApp.class, args);
    }
}
```
````

## Key Points

- **Main takeaway**: Simple explanation
- **When to use**: Practical scenarios
- **Common issues**: What to watch out for

## Links/References

- Video: [video-file-name] ([duration])
- Next: [Next video title]

---

**Created**: [Date]  
**Last Modified**: [Date]

```

## 🤖 Essential Copilot Commands

### 1. Create Note from Transcript
```

/create-note Generate a Spring Boot note using this transcript following my template format:

Template Requirements:

- Simple bullet points (like React notes style)
- Table of contents with "<!-- omit from toc -->" comment
- Clear sections for main topics
- Code examples with brief comments when applicable
- Key points section with main takeaways
- Images referenced inline within relevant sections as ![Description](assets/descriptive-name.png)
- NO separate "Screenshots to Capture" section - integrate image references contextually
- Links/References section with video info and navigation
- Dates at the very end (Created/Last Modified: [Date])
- Use markdown headers for sections

Video Title: [TITLE]
Duration: [DURATION]

Transcript: [PASTE_TRANSCRIPT]

Please organize content logically and place screenshot references inline where they're most relevant to the content being discussed.

```

### 2. Enhance Existing Note
```

/enhance-note Improve this Spring Boot note by:

- Adding missing key points
- Organizing content better
- Suggesting code examples
- Identifying areas for screenshots

Current Note: [PASTE_NOTE_CONTENT]

```

### 3. Extract Code Examples
```

/extract-code From this Spring Boot transcript, extract all code examples and format them as:

- Clean, working code
- Brief comments explaining purpose
- When to use each pattern
- Common variations

Transcript: [PASTE_TRANSCRIPT]

```

### 4. Create Key Points Summary
```

/key-points Create a "Key Points" section for this Spring Boot topic:

- Main takeaway in simple terms
- When to use in real projects
- Common issues to watch out for
- How it connects to other concepts

Topic: [TOPIC_NAME]
Content: [PASTE_CONTENT]

```

### 5. Organize Images and Diagrams
```

/organize-images Help me identify what screenshots/diagrams I should capture for this video and where to place them inline:

- Important visual concepts and their contextual placement
- Code examples worth screenshotting with suggested locations
- Diagrams that explain concepts and where they fit in content flow
- UI/IDE screenshots and their relevant sections
- Terminal outputs and command contexts

Video Topic: [TOPIC]
Transcript: [PASTE_TRANSCRIPT]

Please suggest specific placement within content sections rather than a separate list.

```

### 6. Generate Table of Contents
```

/create-toc Create a table of contents for this Spring Boot note:

- Use markdown links
- Include "omit from toc" comment
- Organize by main sections
- Keep it simple and clean

Note Content: [PASTE_NOTE_SECTIONS]

```

## 📁 File Organization Commands

### 7. Suggest File Structure
```

/organize-files Suggest how to organize these Spring Boot notes:

- Section-based folders
- Naming conventions
- Asset organization
- Cross-references

Current Notes: [LIST_OF_NOTES]

```

### 8. Create Video Index
```

/video-index Create an index of all Spring Boot videos with:

- Video numbers and titles
- Main topics covered
- Difficulty level
- Prerequisites
- Related videos

Course Structure: [PASTE_COURSE_OUTLINE]

```

## 🔧 Workflow Commands

### 9. Pre-Video Preparation
```

/prep-note I'm about to watch this Spring Boot video. Help me:

- Set up note structure
- Identify key concepts to focus on
- Prepare questions to answer
- Plan what screenshots to take

Video: [VIDEO_TITLE]
Course Context: [WHAT_I_LEARNED_SO_FAR]

```

### 10. Post-Video Review
```

/review-note I just finished watching this Spring Boot video. Help me:

- Review my notes for completeness
- Add missing connections to previous topics
- Suggest practice exercises
- Plan next learning steps

My Notes: [PASTE_NOTES]
Video Topic: [TOPIC]

```

## 📊 Progress Tracking Commands

### 11. Weekly Summary
```

/weekly-summary Create a summary of this week's Spring Boot learning:

- Topics covered
- Key concepts mastered
- Code patterns learned
- Areas needing more practice

This Week's Notes: [LIST_OF_NOTES]

```

### 12. Concept Connections
```

/connect-concepts Show how these Spring Boot concepts relate:

- Dependencies between topics
- Practical combinations
- Real-world usage patterns
- Learning progression

Concepts: [LIST_CONCEPTS]

```

## 🎯 Quality Check Commands

### 13. Note Quality Review
```

/quality-check Review this Spring Boot note for:

- Clarity and completeness
- Missing code examples
- Better organization
- Additional explanations needed

Note: [PASTE_NOTE]

```

### 14. Beginner-Friendly Check
```

/beginner-check Make this Spring Boot note more beginner-friendly:

- Simplify complex explanations
- Add more context
- Include analogies
- Highlight prerequisites

Note: [PASTE_NOTE]

```

## 💡 Pro Tips for Using These Commands

1. **Start with `/create-note`** for new video transcripts
2. **Use `/enhance-note`** to improve existing notes
3. **Apply `/organize-images`** before watching videos
4. **Run `/quality-check`** after completing notes
5. **Weekly use `/weekly-summary`** for progress tracking

## 📝 Image Organization Guidelines

### Screenshot Naming Convention:
- `spring-framework-modules.png`
- `dependency-injection-diagram.png`
- `controller-structure.png`
- `jpa-relationships.png`
- `java-version-verification.png`
- `intellij-welcome-screen.png`

### When to Take Screenshots:
- Architecture diagrams
- Code structure examples
- IDE screenshots showing setup
- Error messages and solutions
- Configuration examples
- Terminal command outputs
- Download/installation pages

### Screenshot Placement Strategy:
- **Inline with content**: Place screenshots immediately after the concept they illustrate
- **After code blocks**: Show terminal outputs after command examples
- **During explanations**: Insert UI screenshots while describing interface elements
- **With bullet points**: Add relevant images right after explaining key concepts
- **NO separate sections**: Integrate all images contextually within main content

## 🔄 Workflow Integration

### Daily Routine:
1. Use `/prep-note` before video
2. Take screenshots during video
3. Use `/create-note` after video
4. Apply `/quality-check` before saving

### Weekly Review:
1. Use `/weekly-summary` for progress
2. Apply `/connect-concepts` for understanding
3. Run `/organize-files` for maintenance

---

**Note**: Always customize the generated content to match your learning style and add personal insights!
```
