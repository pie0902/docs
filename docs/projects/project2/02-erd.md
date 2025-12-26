---
title: ERD
---

# ERD (Entity Relationship Diagram)


<img src="/docs/img/project2/hr-erd.png" alt="ERD" />

- Company(companies)를 기준으로 User(users)가 소속되는 구조로, 회사 1 : 사용자 N 관계입니다.
- CompanyRule(company_rule)은 회사별 근무제/출퇴근 기준/허용치를 담는 테이블로 회사와 1:1로 연결됩니다.
- Attendance(attendance)는 사용자별 일자(workDate) 단위 출퇴근 기록이며 사용자/회사에 각각 N:1로 매핑됩니다.
- LeaveRequest(leave_request)는 휴가 신청(기간·타입·상태)을 저장하고 신청자(User)·회사(Company)와 N:1, 승인자(User)는 선택적으로 연결됩니다.
- AnnualLeaveBalance(annual_leave_balance)는 사용자별 연도(year) 단위 연차(부여/사용/잔여)를 관리하며 사용자 1 : 연차잔액 N 관계입니다.