# List of problems detected in Angular online tutorial documentation 
as of the time of creating this file, June 6 2025.

### The removal of word "Component" and introduction of lotsa bugs:
- Commit https://github.com/angular/angular/commit/989e3f0a8811a8e4b9d1c6af9fba9ff14e90e359#diff-6606652fd95a3998d7cccd5d7b29804983545670fbdf0073a33a4de9c0159ad7
- PR https://github.com/angular/angular/pull/61254

### Removal of the references to `@Input()` decorator without the matching description changes
- PR https://github.com/angular/angular/pull/61686

### Removal of the `  standalone: true,` line of code, made a lot of code snippets be mistargeted by 1 line in adev tutorials
- PR https://github.com/angular/angular/pull/58660

#### We've resolved most if not all of the last one with 
- https://github.com/angular/angular/pull/61909 (merged)
- https://github.com/angular/angular/pull/62451 (for v19, unmerged, as no further changes are accepted into v19 branch)
- https://github.com/angular/angular/pull/62457 (awaiting)
