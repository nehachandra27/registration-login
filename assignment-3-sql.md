
select lo_table.user_name,lo_table.activity_name, lo_table.amount, fo_table.first_occurrence, lo_table.last_occurrence from
 (select ua.activity_id activity_id, ua.user_id user_id, ua.amount amount, max(ua.occurrence) last_occurrence, u.name user_name, a.name activity_name 
FROM user_activity ua
LEFT JOIN user u
ON ua.user_id=u.id
LEFT JOIN activity a
ON ua.activity_id=a.id
GROUP BY ua.user_id) lo_table
LEFT JOIN
 (select ua.activity_id activity_id, ua.user_id user_id, ua.amount amount, min(ua.occurrence) first_occurrence, u.name user_name, a.name activity_name 
FROM user_activity ua
LEFT JOIN user u
ON ua.user_id=u.id
LEFT JOIN activity a
ON ua.activity_id=a.id
GROUP BY ua.user_id) fo_table  on (fo_table.user_id=lo_table.user_id)
