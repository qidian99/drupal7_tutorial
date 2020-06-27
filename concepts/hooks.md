# Themes

This results in the following order of execution for a particular theme hook: 

1. template\_preprocess\(\) 
2. template\_preprocesss\_HOOK\(\)
3. MODULE\_preprocess\(\)
4. MODULE\_preprocess\_HOOK\(\) 
5. THEME\_preprocess\(\) 
6. THEME\_preprocess\_HOOK\(\) 
7. template\_process\(\)
8. template\_processs\_HOOK\(\) 
9. MODULE\_process\(\) 
10. MODULE\_process\_HOOK\(\) 
11. THEME\_process\(\) 
12. THEME\_process\_HOOK\(\)

