# Merge-two-sorted-linked-lists
//code starts from here

SinglyLinkedListNode* mergeLists(SinglyLinkedListNode* headA, SinglyLinkedListNode* headB) {
     if (headA == NULL && headB == NULL) {
        return NULL;
    }

    if (headA == NULL) {
        return headB;
    }

    if (headB == NULL) {
        return headA;
    }

    // Ensure that list A starts with the smaller number
    if (headA->data > headB->data) {
        SinglyLinkedListNode *tmp = headB;
        headB = headA;
        headA = tmp;
    }

    SinglyLinkedListNode *listHead = headA;

    while (headB) {
        // Advance through nodes in list A until the next node
        // has data bigger than data at current node of list B
        while (headA->next != NULL &&
               headB->data > headA->next->data) {
            headA = headA->next;
        }

        // Insert current node in list B into list A
        SinglyLinkedListNode* nextB = headB->next;
        headB->next = headA->next;
        headA->next = headB;
        headB = nextB;
    }

    return listHead;


}
