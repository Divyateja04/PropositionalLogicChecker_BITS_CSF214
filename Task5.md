## Task 5: Evaluating the truth value of propositional logic formula in a bottoms up fashion

```c
int recursiveTruthEvaluator(char operation, TreeNode *left, TreeNode *right)
{
    // initializing variables for left sub tree and right sub tree
    // We initialize it to 999 just so that it doesn't mess up by taking initial
    // values as 0
    int leftVal = 999, rightVal = 999;

    if (left != NULL && operation != '~')
    {
        // If left is not alphabet call the function recursively
        if (!isalpha(left->val))
        {
            leftVal = recursiveTruthEvaluator(left->val, left->left, left->right);
        }
    }

    if (right != NULL)
    {
        // If right is not alphabet call the function recursively
        if (!isalpha(right->val))
        {
            rightVal = recursiveTruthEvaluator(right->val, right->left, right->right);
        }
    }

    // If Operation is ~ then we won't have left root
    //  So we don't take left root
    if (operation != '~')
    {
        if (leftVal != 0 && leftVal != 1)
        {
            printf("\nEnter Truth Value for left branch %c: ", left->val);
            scanf("%d", &leftVal);
        }
    }

    if (rightVal != 0 && rightVal != 1)
    {
        printf("\nEnter Truth Value for right branch %c: ", right->val);
        scanf("%d", &rightVal);
    }

    // if both are alphabets, do the operation
    // Switch case taking care of all the possible operations
    switch (operation)
    {
    case '~':
        // printf("\n::>Performing ~");
        return !(rightVal);
    case '+':
        // printf("\n::>Performing +");
        return ((leftVal) | (rightVal));
    case '*':
        // printf("\n::>Performing *");
        return ((leftVal) & (rightVal));
    case '>':
        // printf("\n::>Performing >");
        return ((!(leftVal)) | (rightVal));
    }
}
```