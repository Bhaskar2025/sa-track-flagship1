# D1 Week 2 - Layered Architecture

## What it is - in my own words
- Layered architecture is simple monolith which has controller, service and repository
layers with database. It has separation of concern.

## The four forces - in my own words
- Separation of concern - Each layer has it's own purpose, doesn't interfere with each other. 
- Testability - Each layer can be tested separately. 
- Simplicity - One deployable unit, one codebase, one pipeline. No network calls.
- Familiarity - Simple to understand structure. Industry standard pattern.

## The four failure modes - in my own words
- Big ball of mud - Developer takes shortcuts, skips the layers and code grows. Clean 
separation of concern is not maintained over the time which might create design issue.
- The sinkhole anti-pattern - Simple request passes all four layers without adding values.
- Scalability ceiling - Entire application scales as one unit. different pieces can't be 
scaled separately.
- Deployment coupling - All features deploy together

## When I'd choose layered - one sentence
- Start with layered architecture if team is small. Application which doesn't needs 

## When I'd evolve past it - the specific trigger
- When team split is required.