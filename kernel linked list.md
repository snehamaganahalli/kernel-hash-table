**Kernel linked list**

Initialize the list as below
```
static LIST_HEAD(rtm_neigh_event_list);
```

```
struct vxlan_rtm_neigh_event_data {
   union vxlan_addr rip;
   uint8_t event;
   struct list_head rtm_event_list;
}
```

Get the first entry from the linked list:
```
struct vxlan_rtm_neigh_event_data *rtm_neigh_event_info = list_first_entry(&rtm_neigh_event_list, struct vxlan_rtm_neigh_event_data, rtm_event_list);

i.e list_first_entry(list, type, member);
```

```
struct vxlan_rtm_neigh_event_data rtm_neigh_event_data;
list_add_tail(&rtm_neigh_event_data->rtm_event_list, &rtm_neigh_event_list);
i.e.
list_add_tail(new, head);
```

```
list_empty(struct list *list) 
if (list_empty(&rtm_neigh_event_list)) {
}
```

```
list_del(&rtm_neigh_event_info->rtm_event_list);
```
